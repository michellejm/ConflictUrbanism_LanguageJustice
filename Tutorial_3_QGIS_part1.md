
##Mapping Data Part 1

The purpose of this tutorial is to introduce you to the mapping platform, QGIS, and help you become familiar with the interface and its features. By completing this tutorial, you will be able to:

1. Navigate most commonly used features of the QGIS user interface 
2. Add shapefiles to a project
2. Edit shapefiles 
3. Create a clear and effective map composition
4. Add a vector layer


##Getting Started
Download the GitHub repository for this tutorial. Using the green button [here](https://github.com/michellejm/ConflictUrbanism_LanguageJustice), select `Download ZIP`. The Data folder will then have all of the datasets needed for this tutorial. 

##Mapping Refugee Destinations in the United States

This mapping project is based on recent [discussions](https://www.thisamericanlife.org/radio-archives/episode/600/will-i-know-anyone-at-this-party?act=1") about Refugees in the United States, research on language maintenance and English acquisition by refugees in the [Twin Cities Metropolitan Area](http://onlinelibrary.wiley.com/doi/10.1111/j.0020-7985.2003.00262.x/full) (Fennelley and Palasz, 2003) and the shift in the early 2000's away from refugees being resettled in larger cities towards smaller and mid-sized cities. We are interested in this topic because Refugees in the US tend to speak less common languages (i.e., not English, Spanish, or Chinese), and tend to settle in small enclaves. Unlike other immigrant groups, refugees tend to have less academic and linguistic preparation before arriving in the US and because of a variety of factors, rarely have the opportunity to, or other adult learning opportunities (for more about Refugees in the US, visit [Office of Refugee Services](http://www.acf.hhs.gov/orr).

We are interested in creating a map of refugee resettlement in the United States (and at the same time exploring the QGIS interface). We have a point file for the cities refugees go when they arrive in the United States (from the [Refugee Processing Center](http://www.wrapsnet.org/Reports/InteractiveReporting/tabid/393/EnumType/Report/Default.aspx?ItemPath=/rpt_WebArrivalsReports/MX%20-%20Arrivals%20by%20Destination%20and%20Nationality)) and a polygon file for state boundaries. This map will serve as a basemap to which we can add additional information and layers in order to better understand refugee resettlement in the United States.

##Setting up QGIS

**Launch** QGIS. Your new blank map project will look like this:

![blank](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/01_OpenQGIS.png)

Begin to familiarize yourself with the interface. You can also refer to this [brief description](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Resources/QGIS_InterfaceDescription.md) of the elements of the interface for more information. 

##Adding Layers

Maps in QGIS are based on data layers. This system allows you to analyze datasets with respect to each other. We will use two layers with different information. The basemap is polygons representing states in the US. We will layer 

First we will add a basemap of the United States. 

1. Go to the Data/cb2014 folder. This folder contains all the files QGIS needs to make an outline of the United States. 
	1. You'll notice a number of different file extensions. Do NOT delete, move or rename these files.
	2. These **files must stay together** in the same folder otherwise QGIS will not be able to load the layer.

* .shp - The main file that stores the feature geometry (required).
* .shx - The index file that stores the index of the feature geometry (required).
* .dbf - The dBASE table that stores the attribute information of features (required).
* .sbn and .sbx - The files that store the spatial index of features (these might get corrupted, see note at the end of this tutorial).
* .prj - The file that stores the coordinate system information.
* For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).

2. Click on the `Add Vector Layer` button to add the data. 

![vector](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)

	1. Add the `cb_2014_us_state.shp` file. Even though we only add this file to the map, QGIS still references the other files (.shx,.dbf,.sbn,.prj). 
	
	The selected layer will be added in default colors. 

3. This map looks strange because it is in the wrong Coordinate Reference System (CRS). We need to change the projection. Here's a [simple tool](http://projectionwizard.org/) to help you pick a CRS if you ever don't know which one to pick. 
	1. Double click on the layer to change to CRS. We want "North America Lambert Conformal Conic (EPSG: 102009)" (North America Albert would have been OK, too)

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/CRS.tiff)

	2. Click on the Render box in the lower right hand. Also change this to "North America Lambert Conformal Conic (EPSG: 102009)"
	
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/projection.tiff)

4.  We need to remove these.	
	1. Right click on the map layer and select "Show Feature Count"
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/featurecount.tiff)
	2. The number of polygons will appear next to the layer name.
	3. It should show 56 features, we want 51 polygons (the US plus Washington DC).
	4. Select the layer (so it is highlighted blue).
	5. Click on the Edit pencil near the top.
	6. Zoom in to Puerto Rico (using the Magnifying Glass with a + on it)
	7. Select the 'Select Features by area or single click' button
	8. Click on Puerto Rico to select it - it will change color
	![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/featuresbyarea.tiff)
	9. Click on the Trash can on the left side of the toolbar to delete it.
	10. Repeat for the US Virgin Islands, American Samoa, Guam, and Northern Mariana Islands.
	11. Recenter the map using the Zoom Full Magnifying Glass (the one with the arrows going out of it) 
	12. SAVE!

5. Moving Alaska and Hawaii is beyond the scope of this tutorial. 

6. Add the cities layer. 
	1. Add Delimited Text layer
	
![Delimited](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/Delimited.tiff)

	2. Select the city_latlong.csv file
	3. Select the 'csv' button and make sure that the latitude and longitude columns are the correct ones.
	
	3. If you can't see the points or only see one point, double click on the layer and go to General to make sure that it is the same projection as the map (North America Lambert Conformal Conic (EPSG: 102009)).
	4. If you still can't see them, click on the zoom full magnifying glass (with three arrows pointing outwards), and then zoom back in to the lower 48 states.

7. Moving Layers
	1. Click and drag the states layer on top of the cities layer. The cities points are no longer visible because they are behind the states polygons. 

![order](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/03_Adding_Layers.png)

8. It might be easier to look at if we use state outlines rather than filled polygons. To do this, we must change the **style** of the data layer. 
	1. Double click on the layer name.
	2. The properties box will appear, select the 'Style' tab on the left
	3. Click on Fill > Simple Fill
	4. Select Fill > Transparent and Border > Solid Line
	5. Select 'OK' to exit the menu

![style](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/transfill.tiff)

**Save** your QGIS project by selecting `Project` > `Save`. Name your project Refugee_Cities.qgs and save it in the folder you are using for these tutorials. QGIS projects are saved as .qgs files. It is important to note that the data layers are not saved with it the map project but are rather linked to the project.


__________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered by the [Center for Spatial Research](http://c4sr.columbia.edu) at Columbia University in Spring 2017. 
It is based on the tutorial written by Dare Brawley, for *Mapping for the Urban Humanities* taught in Summer 2016 also by the [Center for Spatial Research](http://c4sr.columbia.edu).






