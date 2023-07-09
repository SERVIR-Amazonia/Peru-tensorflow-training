---
layout: page
title: Integrating TensorFlow with Google Earth Engine
parent: Introduction to ML, Deep Learning and Google Colab
nav_order: 4
---

# Spatial Analysis

QGIS offers a multitude of geoprocessing tools that allow you to manipulate vector and raster data. Elements such as `Buffer`, `Clip`, `Dissolve`, or `Intersection` allow you to create zones surrounding a border, cut the layer by a particular boundary, dissolve a specific inner geographical area, or obtain a common area between two or more layers, respectively. These tools give us a way to extract more insightful analyses from geospatial data.

## Objectives
1. Learn how to use the buffering tool in QGIS.
2. Use the zonal statistics tool to calculate the total population within a particular region.

## Buffering
The `Buffering` tool is one of the most commonly used geoprocessing tools. Practically speaking, it allows you to define two areas: a region that falls within the specified distance, and a region that falls outside of the specified distance. The *buffer zone* is the region that falls within the defined distance. When you establish a buffer, it is important that you check what type of units your data uses. The type of units is defined by the data’s projection. You can check the projection by right-clicking on the layer and going to `Properties > Information` and scroll down to the `Coordinate Reference System (CRS)` section. 

The buffer zone does not have to be defined by a single number – it can vary based on the values defined in a specific Attribute Table column. Furthermore, you can define multiple buffers for a single object, as well as buffers with overlapping or dissolving boundaries.

[IMAGE buffer w variation, multiple buffers, dissolved vs overlapping buffers]

### Exercise 3.1. Delineate historical flood risk extent.
We will visualize flood risk zones by establishing a buffer around the major waterways in Puerto Rico based on historical flood extents.

1. Open the `pr-elev-analysis` project.
2. Ensure that the following layers are loaded into the project:
    1. For analysis: `pr-rivers-corrected-reproj`
    2. For visualization: `PRI_adm0`, `pr-elev-clipped`, `pr-hillshade`.
3. Uncheck any other layers so they are not visible to keep things organized.
4. Double-check that all the layers and the map project are set to the CRS `EPSG:32630` setting (this is important so that we have a projection that uses `meters` as its distance metric). If they are not, you will need to change the CRS:
    1. Navigate to `Processing > Toolbox` and search for `Reproject Layer`. Choose an input vector layer that needs to be changed, and set `EPSG:32630 - WGS 84 / UTM zone 20N` as the `Target CRS`. For raster layers, you will need to use `Rasters > Projections > Warp (reproject)...`.
    2. Choose to save the file as `LAYER-NAME-HERE-reproj` in the `intro-gis-data/analysis` folder.
    3. Press `Run` and then close the window. Save the project.
    4. Repeat steps 1-3 for any other vector layers that need to be reprojected. 
    5. To change the map canvas projection, click on the lower right corner where it says the current projection (most likely `EPSG:4326`). Choose `WGS 84 / UTM zone 20N` and choose `OK`.
    6. Remove any layers in the wrong projection from the map and and adjust the symbology as needed.
5. Navigate to `Processing > Toolbox` and use the search bar to locate the `Tapered buffers` tool listed under the `Vector Geometry` category.
6. Rivers do not flood uniformly. Thus, instead of defining a fixed value to establish the buffer zone, we will use a buffer that gradually increases from the start of the line segment to the end of the line segment such that a greater flood extent is defined at lower elevations. The rivers in the `pr-rivers-reproj.gpkg` file have already been configured so that their start point is at a higher elevation and their end point at a lower elevation. 
7. Define the “Tapered buffers” parameters. 
    1. **Input layer:** `pr-rivers-reproj`
    2. **Start width:** `0.00`
    3. **End width:** `3200.00`
    4. **Segments:** Select the dropdown menu button. Hover over the `Field type: int, double, string` option and select `maxelev`. This choice will create a more gradual looking buffer.
8. Leave the default option to save the layer as a temporary layer as press `Run`, close the window, and save the project.

You should see a new layer called `Buffered` appear on the canvas. You may notice that it looks a little messy – a number of the rivers have overlapping buffer zones. Let’s dissolve the overlapping borders to create a cleaner flood extent boundary. 

### Exercise 3.2. Dissolve buffer boundaries.
1. Navigate to `Vector > Geoprocessing Tools > Dissolve...`
2. Select `Buffered` as the input layer.
3. Next to the `Dissolved` field, select the `...` button and save the file as `pr-flood-extent` in the `intro-gis-data/analysis` folder. 
4. Press `Run` and then close the window. Save the project.

Now you have a layer that indicates the possible flooding extent from rivers in Puerto Rico. Obviously this layer is a very rough flooding estimate, but it will serve our purposes for the remainder of the lesson.

## Zonal Statistics
More than just visualizing data, geospatial analysis requires the ability to gain numerical insights from the data to better understand patterns and trends occurring within the study region and time period. A helpful tool for conducting this type of analysis is the Zonal Statistics tool. This process allows you to calculate the mean, median, sum, minimum, maximum, or range of a particular feature within a specified boundary. The tool is applied to raster data, but the boundary can be specified with vector or raster data. 

[IMAGE zonal stats visualization]

### Exercise 3.3. Calculate total population at risk of flooding.
For our next exercise, we will use the population layer to determine the number of people within the country that fall within the potential flood zone, putting them at risk of being affected by flooding events.

1. Open up the `pr-elev-analysis` project in QGIS if it is not already open.
2. You should have the same layers loaded into the project as in **Exercise 3.1** and **3.2**.
3. Go to `Layer > Add Layer > Add Raster Layer...` and select the `pr-population-2018.tif` file in the `intro-gis-data` folder. Press `Add` and close the window.
4. Check the projection and reproject the layer to `EPSG:32620` if necessary.
5. Now click on `Processing > Toolbox` to open the Toolbox panel. Search for `Zonal Statistics` and double-click on the name to open it. The tool should be listed under the `Raster analysis` category.
6. Set the following parameters:
    1. **Input layer:** `pr-flood-extent`
    2. **Raster layer:** `pr-population-2018-reproj`
    3. **Raster band:** This field should auto populate. Leave it as is.
    4. **Statistics to calculate:** Click the `...` next to the statistics field and check only the `Sum` option. Press `OK` to return to the parameters window.
7. Next to the zonal statistics field, press `...` and save the file in `intro-gis-data/outputs` as `pr-total-pop-flood-risk`.
8. Click `Run` and close the window. Save the project.
9. A new layer called `pr-total-pop-flood-risk` should appear. I will look the same as the `pr-flood-extent` layer, but it contains more information in the attribute table. Right-click on the layer name and select `Open Attribute Table`.
10. Scroll to the right to view the last column in the table `_sum`. This number is the total number of people who live in flood risk zones, or about `651,000` people.

That’s quite a few people! If you wanted to know the number of people for each river feature, you could run the same operation on the non-dissolved buffer layer. 

### Challenge: Calculate percentage of national population at risk for flooding.
See if you can take the analysis one step further – you know the number of people who live within flood risk zones, but what percentage of the population is that? Knowing that value could aid in resource allocation or population relocation. Calculate the percentage of the national population that falls within our defined flood risk zones. 
* *Hint 1: Calculate the total country population and join it to the layer from Exercise 3.3*
* *Hint 2: The tools `Join attributes by field value` and the `Field calculator` will be useful in this exercise.*

**Congratulations!** You completed the Introduction to GIS workshop. You can refer back to this material anytime you want throughout the learning series, and don’t forget to reach out with feedback or questions!
