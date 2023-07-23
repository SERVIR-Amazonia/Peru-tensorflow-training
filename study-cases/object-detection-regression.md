---
layout: page
title: Selective Logging Detection with Deep Learning
parent: ACCA's Case of Study
nav_order: 1
---

# Introduction
Welcome to an Introduction to GIS with QGIS! This workshop will give an overview of general foundations of QGIS, an open-source GIS software for vector and raster analysis. To start off, this section will cover a number of fundamental GIS concepts, provide a snapshot of key geoprocessing tools, and point out high-quality geospatial data to be aware of and how to access it throughout the next few modules. 

## Set-up
1. [Install](https://www.qgis.org/en/site/forusers/download.html) QGIS if not already installed.
2. [Download](https://drive.google.com/drive/folders/1zIV-ADnNxFNIDcDPvQPu8nmE5X9esnvl?usp=share_link) and upzip the data folder for the lesson. Save the upzipped folder on your Desktop. Make sure the folder is named `intro-gis-data`.

## Objectives
1. To show the potential of QGIS as a powerful decision-making tool to policy officers.
2. To teach occasional GIS users a set of basic and advanced operations for managing, manipulating and presenting vector and raster data in QGIS.
3. To demonstrate to experienced GIS staff that QGIS can be a valid alternative – at no cost – to licensed geospatial software.

## Why QGIS?
There are a number of reasons why someone (and why we in this workshop!) would choose to use QGIS for geospatial analysis. 
1. **It’s free, as in lunch.** Installing and using the QGIS has no initial fee and recurring fee.
2. **It’s free, as in liberty.** If you need extra functionality in QGIS, you can do more than just hope it will be included in the next release. 
3. **It’s constantly developing.** Because anyone can add new features and improve on existing ones, QGIS never stagnates.
4. **Open source = lots of documentation.** Extensive help and documentation is available.
5. **Cross-platform.** QGIS can be installed on MacOS, Windows and Linux.

Fundamentally, QGIS is open source software. In recent years, there has been a large push to “democratize” data by encouraging the use and development of open source data, software, and scripts. NASA has declared 2023 the [Year of Open Science](https://science.nasa.gov/open-science/transform-to-open-science#:~:text=Within%20the%20TOPS%20mission%2C%20NASA,will%20shift%20the%20current%20paradigm.), and the UN has cited the movement towards open data management as key for innovation and the economic enhancement of nations in its 3rd edition draft of [Future Trends in Geospatial Information Management: the 5-10 year vision](https://ggim.un.org/documents/DRAFT_Future_Trends_report_3rd_edition.pdf). Using QGIS furthers this movement and opens up the geospatial world to more than those who can afford it. 

## QGIS Interface
We will explore the QGIS user interface so that you are familiar with the menus, toolbars, map canvas and layers list that form the basic structure of the interface before beginning the exercises in this lesson.

[IMAGE qgis interface]

The elements identified in the figure above are:
1. **Layers List / Browser Panel**
> In the **Layers** list, you can see a list, at any time, of all the layers available to you. Expanding collapsed items (by clicking the arrow 
> or plus symbol beside them) will provide you with more information on the layer’s current appearance. Hovering over the layer will give you
> some basic information: layer name, type of geometry, coordinate reference system, and the complete path of the location on your device. Right-
> clicking on a layer will give you a menu with lots of extra options. You will be using some of them before long, so take a look around!  
> 
> The QGIS **Browser Panel** is a panel in QGIS that lets you easily navigate files stored in your database. You can access to common vector
> files (e.g. ESRI Shapefile or MapInfo files), databases (e.g. PostGIS, Oracle, SpatiaLite, GeoPackage or MSSQL Spatial) and WMS/WFS 
> connections. If you save a project, the Browser Panel will also give you quick access to all the layers stored in the same path of the project
> file under the Project Home item.
2. **Toolbars**
> The most often used sets of tools can be turned into toolbars for basic access. For example, the `File` toolbar allows you to save, load,
> print, and start a new project. You can easily customize the interface to see only the tools you use most often, adding or removing toolbars as
> necessary via the `View > Toolbars` menu.
> Even if they are not visible in a toolbar, all of your tools will remain accessible via the menus. For example, if you remove the `File`
> toolbar, you can still save your map by clicking on the `Project Menu` and then on `Save`.
3. **Map Canvas**
> This is where the map itself is displayed and where layers are loaded. In the map canvas you can interact with the visible layers: zoom in/out,
> move the map, select features and many other operations that we will explore further in the next sections.
4. **Status Bar**
> Shows you information about the current map. Also allows you to adjust the map scale, the map rotation and see the mouse cursor’s coordinates
> on the map.
5. **Side Toolbar**
> By default the side toolbar contains the buttons to load the layer and all the buttons to create a new layer. Remember that you can move all
> the toolbars wherever it is more comfortable for you, so you may not have a toolbar here.
6. **Locator Bar**
> Within this bar you can access almost all of the objects within QGIS: layers, layer features, algorithms, spatial bookmarks, etc. Check all the
> different options in the Locator Settings section of the [QGIS User Manual](https://docs.qgis.org/3.22/en/docs/user_manual/index.html).






