---
layout: page
title: Making a Map with Vector Data
parent: Introduction to GIS with QGIS
nav_order: 2
---

# Making a Map with Vector Data
In this module, you will create a basic map which will be used later as a basis for further demonstrations of QGIS functionality.

## Objectives
1. Add layers and start building an example map.
2. Navigate the Map Canvas.
3. Understand symbology.

## Vector Data
**What is vector data?** Vector data provide a way to represent real world features within the GIS environment. Vector features have *attributes* (stored in attribute tables), which consist of text or numerical information that describe the features. A vector feature has its shape represented using a *geometry*. The geometry is made up of one or more interconnected vertices. The organization of the vertices determines the type of vector that we are working with: point, line, or polygon. A *vertex* describes a position in space using an X, Y and an optional Z axis. The X and Y values will depend on the *Coordinate Reference System (CRS)* being used. A CRS is a way to accurately describe where a particular place is on the earth’s surface. One of the most common reference systems is the WGS84 *longitude* and *latitude* framework. Lines of longitude run from the North Pole to the South Pole. Lines of latitude run from the East to West. You can describe precisely where you are at any place on the earth by giving someone your longitude (X) and latitude (Y). You can transform data from one CRS to another to maintain continuity between data sets, which is important for analysis.

## Vector Data Format
Vector data can come in many different formats. For this workshop, we will use the Shapefile format (`.shp`) that stores the geographic coordinates of each vertex in the vector, as well as metadata including:
* **Extent:** the spatial extent of the shapefile (i.e. geographic area that the shapefile covers). The spatial extent for a shapefile represents the combined extent for all spatial objects in the shapefile.
* **Object type:** whether the shapefile includes points, lines, or polygons.
* **Coordinate reference system (CRS)**
* **Other attributes:** for example, a line shapefile that contains the locations of streams might contain the name of each stream.

Because the structure of points, lines, and polygons are different, each individual shapefile can only contain one vector type (all points, all lines or all polygons). You will not find a mixture of point, line and polygon objects in a single shapefile.

[IMAGE points lines polygons]

### Exercise 1.1. Initialize the study area map.
For this exercise, we will make a study area map of the island of Puerto Rico. You can skip step 1 - that part was already done for you! It is written out for your reference on how to collect data.

1. *You can skip this step.* Go to the [DIVA-GIS website](https://diva-gis.org/gdata) and search for `Puerto Rico`. 
    1. Download administrative boundaries, rivers (inland water), roads, population, and elevation.
    2. Extract the zip files to the data folder stored in your training directory.
2. Open QGIS and start a new project. You will have a new, blank map. Save the project in the `intro-gis-data/analysis` folder and name it `pr-study-area-map`.
3. The Data Source Manager dialog allows you to choose the data to load depending on the data type. We’ll use it to load our dataset: click the [IMAGE data source button] `Open Data Source Manager` button.
4. Load in the initial vector data.
    1. In the `Data Source Manager` window, select the `Vector` tab. 
    2. Select `File` as the `Source Type`.
    3. Press the `...` button next to `Vector Dataset(s)`. 
    4. Navigate to `intro-gis-data/PRI_adm` and select the `PRI_adm0.shp` file. Click `Open`. The file should now be loaded in the `Data Manager` window. [IMAGE loaded vector file]
    5. Press `Add`. Now repeat steps 3 and 4 to load in the `PRI_adm1.shp` file. Once you have added both files, press `Close` to close the window. Save the project. [IMAGE loaded adm layers]

Databases allow you to store a large volume of associated data in one file. You may already be familiar with a database management system (DBMS) such as Libreoffice Base or MS Access. GIS applications can also make use of databases. The `GeoPackage` open format is a container that allows you to store GIS data (layers) in a single file (e.g. ESRI Shapefile format). A single `.gpkg` file can contain various data (both vector and raster data) in different coordinate reference systems, as well as tables without spatial information; all these features allow you to share data easily and avoid file duplication.

### Exercise 1.2. 
In order to load a layer from a GeoPackage, you will first need to create the connection to it:
1. Open the `Data Source Manager`.
2. On the left, click on the  `GeoPackage` tab.
3. Click on the `New` button and browse to the `pr-cities-towns.gpkg` file in the `intro-gis-data` folder.
4. Select the file and press Open. The file path is now added to the Geopackage connections list, and appears in the drop-down menu.

Now that you have established a connection to the file, you can add the layer to the map canvas.

5. Press `Connect`. In the central part of the window you should now see the list of all the layers contained in the GeoPackage file.
6. Select the `pr_large_cities` layer and press `Add`. The selected layer is added to the Layers panel with features displayed on the map canvas.
7. Press `Close` to close the window. Save the project.

[IMAGE added geopackage]

There are other types of data layers that you can add to the QGIS map canvas, as evidenced by the different tabs in the `Data Source Manager`. Learn more about these types in the [QGIS User Manual](https://docs.qgis.org/3.22/en/docs/user_manual/index.html).

You can choose to turn layers on and off by clicking on the checkbox next to the layer name, or reorder the layers by dragging the name to your desired spot. The layers are displayed in the order that they are listed (i.e., top of the list of layers displayed on top and vice versa). 

## Symbology
The symbology of a layer is its visual appearance on the map. The basic strength of GIS over other ways of representing data with spatial aspects is that with GIS, you have a dynamic visual representation of the data you’re working with. The end user of the maps you produce should easily understand what the map represents. 

### Exercise 1.3. Customize the study area map.
Before we customize the colors and structures, let's add a bit more context to the map. 
1. Follow the instructions from **Exercise 1.1** to add `intro-gis-data/PRI_wat/PRI_water_lines_dcw.shp` and `intro-gis-data/PRI_rds/PRI_roads.shp` to the map canvas. [IMAGE rivers roads]

To change a layer’s symbology, open its `Layer Properties`. Let’s begin by changing the color of the `PR_adm0` layer.

2. First, turn off the `PR_adm1` layer by unchecking the box next to its name.
3. Right-click on the `PR_adm0` in the layers list.
4. Select the `Properties...` option in the menu that appears. Alternatively, you could also access a layer’s properties by double-clicking on the layer in the Layers list.
5. In the `Layer Properties` window, select the `Symbology` tab. Click on the element `Simple Fill` below the `Fill` dropdown at the top of the window.
6. Next to `Fill Color`, select a color to fill in the Puerto Rico boundary layer. [IMAGE color customization]
7. You can press `Apply` to test out the color you chose, or else just press `OK` to save the customization.
8. Repeat steps 3-7 to change the colors for the `pr_large_cities`, `PRI_roads`, and `PRI_water_lines_dcw` layers.

You can also change the structure of a layer, i.e., how the layer object appears. Next, let's change the appearance of the `PRI_roads` layer.

9. Follow steps 3-5 to open the `Symbology` tab for the `PRI_roads` layer.
10. Click on the dropdown menu next to the `Stroke Style` field and choose the `Dash Dot Line` option. Press `OK`. Save the project.

Finally, let's add labels to the cities layer so it's easier to read the map.

11. Right-click on `pr_large_cities` and choose `Properties...`.
12. Click on the `Labels` tab.
13. Click on the dropdown menu at the top of the window and choose the `Single Labels` option. 
14. Next to the `Value` field, choose `name`. 
15. In the `Text` tab option, set `10.0` as the font size.
16. Click on the `Placement` tab within the `Labels` window and increase the `Distance` field to `0.1000`. Press `OK`.

Now that you’ve got a map, you need to be able to print it or to export it to a document. Both exporting and printing is handled via the Print Layout. QGIS allows you to create multiple maps using the same map file. For this reason, it has a tool called the Layout Manager.

### Exercise 1.4. Generate a printable map layout and export as a PDF.
1. Click on the `Project > Layout Manager...` menu entry to open the tool. You’ll see a blank Layout manager dialog appear. [IMAGE blank layout manager]
2. Under `New from Template`, select `Empty layout` and press the `Create...` button. You could also create this new layout via the `Project > New Print Layout...` menu.
3. Name the new layout `pr-study-area-map` and click `OK`.
4. You will now see the Print Layout window: [IMAGE blank print layout window]
5. Right-click on the sheet in the central part of the layout window and choose `Page properties...` in the context menu.
6. Check that the values in the `Item Properties` tab are set to the following: 
    1. **Size:** A4
    2. **Orientation:** Landscape.
7. Now you’ve got the page layout the way you wanted it, but this page is still blank. It clearly lacks a map. 
8. Click on the `Add Map` button. With this tool activated, you will be able to place a map on the page.
9. Click and drag a box on the blank page. The map will appear on the page.
10. Go to the `Layout > Save Project`. This is a convenient shortcut to the one in the main dialog.

Now, add the title.

11. Click on the `Add Label` button.
12. Click on the page, above the map, accept the suggested values in the `New Item Properties` dialog, and a label will appear at the top of the map.
13. Resize it and place it in the top center of the page. It can be resized and moved in the same way that you resized and moved the map. However, there is also an `Alignment` tool in the `Actions Toolbar` to help position the title relative to the map (not the page).
14. Select the label by clicking on it.
15. Click on the Item Properties tab in the side panel of the layout window.
16. Change the text of the label to **Puerto Rico Rivers, Roads, and Major Cities**.
17. Use this interface to set the font and alignment options under the `Appearance` section.

Next, add a legend.

18. Click on the `Add Legend` button.
19. Click on the page to place the legend, accept the suggested values in the `New Item Properties` dialog.
20. A legend is added to the layout page, showing layers symbology as set in the main dialog. As usual, you can click and move the item to where you want it.
21. In the `Item Properties` tab, you’ll find the `Legend Items` group.
22. Uncheck the  `Auto update` box, allowing you to directly modify the legend items. Remove the `PR_adm1` layer from the legend by clicking the red minus sign.
23. You can also rename items. Select a layer from the same list. Double-click on the layer. Rename the layers to Land, Roads and Streets, Surface Water, Rivers, etc.

Finally, add a north arrow and scale bar.

24. Click on the `Add North Arrow` button.
25. Drag a box where you want the north arrow to appear.
26. Click on the `Add Scale Bar` button.
27. Drag a box where you want the scale bar to appear.

Finally, the map is ready to export! Click on the `Export as PDF` button and save the file in `intro-gis-data/outputs` as `pr-study-area-map`. Click `Save` if a pop-up box appears. Close the window.

