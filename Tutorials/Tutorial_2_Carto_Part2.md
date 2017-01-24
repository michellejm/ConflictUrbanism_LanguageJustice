# Carto Tutorial - Part 2 Adding your own data

By the end of this tutorial, you will be able to:

* Add points to a basemap manually and from a spreadsheet.
* Geocode a group of addresses.
* Make decisions about how to display information on your map.
* Decide on ways to capture new data
* Import data from Open Street Map into your own map.


The assumption in this tutorial is that you have collected raw data from the world and want to represent it on your map. There are a lot of things you can do with that data, including labeling it in a creative, provocative, or alternative ways, geocoding it to find latitude and longitude, aligning it to other information about the physical or social space it inhabits. 

First thing, though, we have to get that data onto the map. Though there are many ways to represent shapes on a map, we are going to start with dropping pins and getting latitude and longitude. Determining the latitude/longitude of a point is referred to as "geocoding." Addresses, points, intersections, events, etc. can all be geocoded and therefore represented as latitude and longitude.  Carto does this automatically when you place a point on a map. 

## Part I - Adding individual points

1. Go to the Carto Dashboard and click on 'New Map' in the upper right hand corner.
![newmap](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/newmapcarto.png)
2. You will arrive on a page to add datasets. Click on 'Create Empty Map' on the right side of the page.
![createempty](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/createempty.png)
3. You will be prompted to add 'Points', 'Lines', or 'Polygons'. Select **'Point'**
	1. Alternatively, 'Skip' and then click on the little bubble in the lower right hand corner
	![addfeature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/addfeature.png)
4. In this tutorial, we are first going to map language information about Columbia University. For each combination, drop a pin on the building (if you don't know the shape of the building, just drop a point somewhere on campus). The map is at Zoom Level 17 - which shows the details of the buildings. 
	1. Schermerhorn Extension, Center for Spatial Research, English
	![schermerhorn](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/schermerhorn.png)
	2. Butler Library, Ancient & Medieval Studies Reading Room, Ancient Greek
	3. International Affairs Building, Language Resource Center, Yoruba
5. Toggle to DataView to add the relevant information about the pin you just dropped (double click on the box to edit it). ![featureedit](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/schermerhorn.png)
6. Latitude and Longitude should appear for each of these locations. 

Clearly this is a tedious way of making a map, let's try something more efficient.

## Part II - Geocoding batches of addresses

We are going to geocode language information from a spreadsheet. This data was collected from various sources, and may be similar to the type of data you will be collecting in your projects. We will use the Geocoder provided by the [US Census](https://www.census.gov/geo/maps-data/data/geocoder.html). Carto will geocode up to 100 points for free.

1. Go to the [data folder], and find the ColumbiaLanguages.csv file and save it to your computer (click 'View Raw'. If you are on a Mac, click `Command + s` to save it. On a PC, select it all and save it to a Text Document (in Notepad, Text Wrangler, or Sublime)).
2. This file is already formatted for you. To use the Census Geocoder, the file must be in .csv format, and include the following information:
	1. Unique ID,
    	2. House Number and Street Name,
    	3. City,
    	4. State,
    	5. ZIP Code
2. Visit [Census Geocoder](https://geocoding.geo.census.gov/geocoder/)
3. Select Find Locations Using... Address Batch
4. Select `Public_AR_Current`
4. Upload the ColumbiaLanguages.csv file.
5. A csv file will be returned that looks something like this, though it may not be in the same order:
![csv](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/address.png)
6. To use this file in Carto, we have to clean it. 
	1. Open GeocodeResults.csv in Excel
	2. You may notice that the language and department data is missing. Don't worry about that yet, we will come back to it.
	3. Select the column that looks like Latitude, Longitude numbers (probably Column F)
	4. On the Data Tab, select Text to Columns
	![txtcol](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/latlongtxtcol.png)
	5. Select 'Delimited' and 'Comma' as prompted
	6. Save this file
	7. Optional: I prefer to remove columns that I won't be using before I enter it into Carto:
		1. If they are all a 'Match', remove 'Matching Result 1.' If they are not all a 'Match', inspect the ones that are not and then remove the column. 
		2. If they are all 'Exact', remove 'Matching Result 2' Inspect any fields that are not 'Exact' before removing the column.
		3. The first address column. If everything is an 'Exact Match', the second address column is redundant. If they are not an 'Exact Match', the second address column is the address used to obtain latitude and longitude. You likely want to keep both columns in this case. 
		4. Save the new, clean file
7. Return to Carto and Create a New Map. Select 'Connect Dataset' and upload the GeocodeResults.csv that you just cleaned.
8. Go to data view and make sure it looks like what you expect. At this stage, it may be easier to rename the columns with something you can recognize. If you don't want to do this, write down which field latitude and longitude are in. 
9. Now we need to tell Carto what the Latitude and Longitude columns are so it can plot the points. 
	1. Click `Edit` and `Georeference Layer`
	2. You will be prompted to select which column has Longitude and which has Latitude.
	3. Return to Map View and zoom in on Columbia, you should see your points
10. At this point, these are just points without any information attached. We need to add the language information that we have in the ColumbiaLanguages.csv file.
	1. Return to your Carto Dashboard, and find `Your Datasets`
	2. Add a `New Dataset`
	3. Connect the `ColumbiaLanguages.csv` dataset
	4. Once it appears in the DataView, select `Edit` and `Merge with Dataset`
	5. Merge it with the `GeocodeResults` dataset, and join on the `ID` column
	6. Once the datasets are merged, go to the MapView
11. Now the information that you would have collected in a spreadsheet about each language and department is attached to the markers. 

## Part III - Representing this data

Because there is no statistical or numerical data associated with this map, the best way to represent this data is either simple points or clusters. Simple points allow you to turn on the click or hover feature where you can display information about each point. Clusters represent how many lines are represented at each location. 

If you choose to display the data and want to have each point displayed, but slightly askew from each other so that it appears that they are in slightly different locations in the same building, you may have to manually manipulate the data.
1. Click on DataView and select the line you wish to move over just slightly. 
2. Change either latitude or longitude by approximately .000025, this is just enough to move the location over and be able to see both dots. Of course, if you want it somewhere else, feel free to move it more or less. 
3. Check your work in MapView


## Part IV - Exporting the Map for use in the Case Study

1. In the Map View, click on 'Publish' 

![publish](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cartopublish.png)

2. Select the 'Embed' Option

![embed](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/embedcarto.png)

3. Paste this iFrame Code where you want it to appear in your site.



Congratulations!! That's the second map about language in New York City! 

To complete the Tutorial, email the link to Michelle (instructions on how to download the map are at the end of the [Carto 1 Tutorial](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_1_Carto_Part1.md)

The next part is optional if you think you will want to use data from Open Street Maps (i.e., restaurants, cafe's, schools, yoga studios, etc.).



## Part V - Going Further - Using Open Street Map Data
[Open Street Map](http://www.openstreetmap.org/) is an open source, free, editable map of the world (kind of like the wikipedia of mapping). Click [here](http://www.openstreetmap.org/welcome) for more on the basics of OSM
Users contribute data to the map (i.e., indicating restaurants, marking streets or hiking trails, etc.) There is a lot of data available from OSM that has been contributed by individuals. We are going to download some of it for use in our map. 

1. Go to [Open Street Map](http://www.openstreetmap.org/)
	1. You may need to navigate to [Columbia University](http://www.openstreetmap.org/#map=17/40.80797/-73.96036) and zoom in so you can see all of the Morningside Heights campus and enough detail that the buildings are labeled (zoom level 17).
	2. Initially, there is no information, just a basemap. We are going to Export the data. 
2. Click `Export` 
![export](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/exportdata.png)
3. A default size will be chosen for you. You can edit this by selecting 'Manually select a different area' and dragging the edges of the box to surround what you are interested in. 
![manuallyselect](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/manually.png)
4. Select Export and save it to your computer. 

Now we want to upload this data into Carto so we can analyze and visualize it. 

1. Return to your Carto Account.
2. Go to the Data View and select `New Dataset`
![newdata](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/newdata.png)
3. Upload the map.osm file from your computer
4. Return to the DataView and inspect this new dataset. 
5. Switch to map view to get a sense of what information is positioned where. 

There is a lot of information here. We are not interested in all of it. Let's look only at the Cafe's. 

1. Open the `SQL` Editor on the left hand side
2. We want to SELECT everything FROM the dataset, map_points, WHERE elements in the column, 'other_tags' is LIKE "amenity"=>"cafe" 
![sqlselect](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/sqlosm.png)
	1. '[LIKE](https://www.postgresql.org/docs/8.3/static/functions-matching.html)' means that the target string is in the entire string. 
	2. 'ILIKE' is case-INSENSITIVE 'LIKE'
	3. The % % on either end are a [Regular Expression](http://www.regular-expressions.info/). They mean 'Wildcard', so anything can come before or after the target string.
	
3. Return to the DataView
SELECT * FROM map_points WHERE other_tags ILIKE '%"amenity"=>"cafe"%'


Congratulations! You have now uploaded OSM data into a Carto Map. You can, of course, do much more with this (i.e., concentration of cafes versus [candy store](http://gothamist.com/2014/05/02/ask_a_native_new_yorker_whats_the_d.php) ('bodega','deli', 'corner grocery', etc.) in a given language neighborhood, etc. 






