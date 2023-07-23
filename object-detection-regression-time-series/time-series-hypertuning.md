---
layout: page
title: Time Series Analysis and Hypertuning
parent: Object Detection, Regression, Time Series Analysis
nav_order: 3
---

# Making a Map with Raster Data

Raster data is quite different from vector data. Vector data has discrete features with geometries constructed out of vertices, and perhaps connected with lines and/or areas. Raster data, however, is like any image. Although it may portray various properties of objects in the real world, these objects don’t exist as separate objects. Rather, they are represented using pixels with different values.

## Objectives
1. Learn how to work with raster data in QGIS.
2. Use raster data to create a DEM and Hillshade map.

## Raster Data
**What is raster data?** Raster data is any pixelated (or gridded) data where each pixel is associated with a specific geographical location. The value of a pixel can be continuous (e.g. elevation) or categorical (e.g. land use). A geospatial raster is accompanied by spatial information that connects the data to a particular location. This includes the raster’s extent and cell size (resolution), the number of rows and columns, and its coordinate reference system (or CRS). The spatial extent is the overall geographic coverage of the spatial object (edge or location that is the furthest north, south, east and west). A resolution of a raster represents the area on the ground that each pixel (cell size) of the raster covers.

[IMAGE raster data]

**How is raster data stored?** Raster data can come in many different formats, from a standard file-based structure of `TIFF`, `JPEG`, `ASC`, `PRJ`, `CLR`, etc. to binary large object (`BLOB`) data stored directly in a relational database management system (`RDBMS`). 

### Exercise 2.1. Create a DEM and hillshade map. 
1. Open QGIS and start a new empty project. Save the project in the `intro-gis-data/analysis` folder and name it `pr-elev-analysis`.
2. Add the `PRI_adm0.shp`.
3. Right-click on `PRI_adm0` and select `Properties...`.
4. Select the `Symbology` tab and then click on `Simple Fill`.
5. Next to the `Fill style` and select the `No brush` option. Press `OK`.

Now, we can add the SRTM elevation data. The SRTM data can be added indirectly or directly in QGIS. The indirect way uses the SRTM data provided by CGIAR and produces a 90 m resolution DEM. The direct way uses SRTM data from NASA and gives a 30 m resolution. The indirect method is faster. Those who have an EarthData login can use the NASA EarthData website and download the SRTM directly in QGIS. Both methods are described below for future reference, though the data has already been downloaded for you and can be found in `intro-gis-data/PR_SRTM`.

#### Indirect Download
1. Go to the (CGIAR SRTM website)[https://srtm.csi.cgiar.org/srtmdata/)].
2. Select the tiles that cover your area of interest. [IMAGE srtm tiles]
3. Click on `Search`.
4. Download the SRTM tiles that cover the study area.
5. Extract the zip files to your folder of choice.
6. Add the SRTM tiles to QGIS.

#### Direct Download
1. Go to https://urs.earthdata.nasa.gov/ and login.
2. To download SRTM data directly in QGIS, the SRTM downloader plugin has to be installed first.
3. Go to `Main Menu: Plugins > Manage and Install Plugin > Search for SRTM Downloader > Install Plugin`.
4. Start the SRTM Downloader plugin: `Plugins > SRTM Downloader > SRTM Downloader`
5. Click on: Set canvas extent, set the output path to your folder of choice, and click on `Download`.
6. A popup window will appear to login to US EarthData.
7. Click on: `Set canvas extent`, and set the output path to your destination folder, and click on `Download`.
8. A popup window will appear to login to US EarthData.

Now, let's continue the exercise and add the DEM data to the map.

1. Click on the `Data Source Manager` button and select the `Raster` tab. 
2. Navigate to `intro-gis-data/PR_SRTM` and select the `srtm_23_09.tif` file.
3. Click `Add` and close the window.
4. Clip the SRTM layer with the boundaries of Puerto Rico. Go to `Main Menu > Raster > Extraction > Clip Raster by Mask Layer`. Select `srtm_23_09` as the input file, and `PRI_adm0` as the `Mask layer`.
5. Choose the `Project CRS` as the `Target CRS`, and uncheck the box next to `Match the extent of the clipped raster to the extent of the mask layer`. Choose to save the file as `pr-elev-clipped` in the `intro-gis-data/outputs` folder.
6. Click `Run` and close the window. Save the project.
7. Open the `srtm_23_09` layer properties and select the `Information` tab. Under the `Information from provider` section, scroll down to view the **Pixel Size**. It should be about `0.0008333`, or around `90` meters around the equator.
8. Remove the `srtm_23_09` layer.

Next, change the symbology for a better visualization of the elevation.

1. Navigate to the `Symbology` tab of the `srtm_23_09` layer properties window.
2. Next to the `Render type` field, choose `Singleband pseudocolor`. 
3. Choose a predefined color ramp from the `Color Ramp` dropdown menu, or select `Create new color ramp...` from the `Color ramp` dropdown menu and select `Catalog: cpt-city` and press `OK`.
4. From here, select the `Topology` tab to select options specfically designed for elevation visualization. Select one and press `OK` to close the pop-out window.
5. Click on the `Transparency` tab. Adjust the `Global Opacity` to `50%`, then press `OK` to close the `Properties` window. Save the project.

### Exercise 2.2. Create/calculate hillshade.
The DEM layer shows you the elevation of the terrain, but it can sometimes seem a little abstract. It contains all the 3D information about the terrain that you need, but it doesn’t look like a 3D object. To get a better impression of the terrain, it is possible to calculate a hillshade, which is a raster that maps the terrain using light and shadow to create a 3D-looking image.

1. To create a hillshade, we are going to use algorithms in the `Raster > Analysis > Hillshade`.
2. Select `pr_elev_clipped` as the input layer.
3. The algorithm allows you to specify the position of the light source: Azimuth has values from `0` (North) through `90` (East), `180` (South) and `270` (West), while the Vertical angle sets how high the light source is (`0` to `90` degrees).
4. We will use the following values: 
    1. **Z factor:** `1.0`
    2. **Azimuth (horizontal angle):** `300.0°`
    3. **Altitude (vertical angle):** `40.0°`
5. Choose to save the file as `pr-hillshade` in the `intro-gis-data/outputs` folder. Click `Run` and close the window.
6. Change the symbology settings so that the hillshade layer enhances the elevation layer with a semi-3D effect. Explore the options: `Blending mode`, `Brightness`, `Gamma`, `Contrast`, and `Saturation` in the `Layer Rendering` portion of the `Symbology` tab in the `Properties` window.
7. Click `OK` and save the project. [IMAGE final elevation and hillshade]

### Challenge: Customize the DEM and hillshade map.
A hillshade can also be used for aesthetic purposes, to make the map look better. The key to this is setting the hillshade to being mostly transparent. Additionally, it can be helpful to add contextual features to the map to ensure that the user can interpret it more easily. 

1. Click and drag the `pr-elev-clipped` layer to be beneath the `pr-hillshade` layer in the Layers panel.
2. Set the hillshade layer to be transparent by clicking on the `Transparency` tab in the `Layer Properties` window.
3. Set the `Global opacity` of the hillshade layer to `50%`.  If the effect doesn’t seem strong enough to you, you can update that value to one of your choosing.
4. Add lakes, rivers, and large cities to the map.
5. Export the map as a PDF with a title, legend, north arrow, and scale bar.
6. Save the project when you are done.
