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

1. In this tutorial, we are first going to map language information about Columbia University. This is the data we have collected about some langauges that can be found at Columbia.
	1. Schermerhorn Extension, Center for Spatial Research, English
	![schermerhorn](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/schermerhorn.png)
	2. Butler Library, Ancient & Medieval Studies Reading Room, Ancient Greek
	3. International Affairs Building, Language Resource Center, Yoruba
2. Go to the Carto Dashboard and click on 'New Map' in the upper right hand corner.
![newmap](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cnewmap.png)
2. You will arrive on a page to add datasets. Click on 'Create Empty Map' on the right side of the page.
![createempty](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/createempty.png)
3. An empty (untitled) layer will be added to your map. 
![untitled](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cuntitledlayer.png)
4. To change the name of this layer, click on the dots next to "untitled_table" and rename it, I'm going to call it "Columbia Languages"
5. Click on the title to go to the editing view
6. It will take you to the data tab.
	1. This icon with the + sign should be visible in the lower right corner. If it isn't, refresh your browser.
	![point](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddpoint.png)
	2. Click on that icon. It will prompt you to drop a pin. 
	3. Drop a pin on the Schermerhorn Extension (data point #1) (if you don't know the shape of the building, just drop a point somewhere on campus). The map is at Zoom Level 17 - which shows the details of the buildings. 
	4. It should take you to this view, where you can enter the attribute name (Schermerhorn Extension) and a description (English)
	5. It will prompt 'Add Custom Value' - click on that, it will not add automatically.
	![featureedit](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cdroppoint.png)
	5. Add the other two data points from Step 1. 
7. Return Home with the small white circle
![home](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/chome.png)
8. Select DataSets View. 
6. Latitude and Longitude should appear for each of these locations. 
	1. Select the table we just made
	2. Add a Column to enter more information
	3. Edit a cell by clicking on it
	![home](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddcolumn.png)
9. Select 'Create Map'
10. You may have to search for the pins. Search New York City in the searchbar at the bottom and find Columbia University. 

Let's hypothesize about areas of influence. Let's assume that the Spanish speaker we found at Schermerhorn Extension is willing to walk up to 50 meters from where he works to get lunch or coffee. We want to know what his area of influence is, or where he carries his Spanish. 

1. Select 'ADD ANALYSIS'
![add analysis](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddanalysis.png)
2. Select 'Create Areas of Influence'
	1. Select the distance you want to use (Time requires having timeseries data in your dataset).
	2. 'Intact' means the spheres will overlap. 'Dissolved' means they turn into one big odd shape
3. However you've selected to make the buffers, change the name of the map to something more recognizable.
4. Share the map
	1. Accessible with the link
	2. Published
	3. Send this link to Michelle at mam2518@columbia.edu

Congratulations! You have added buffers to your map to represent Spheres of Influence


You probably won't collect you data in Carto - it is more likely that you will use a Spreadhseet of some sort. 

## Part II - Geocoding batches of addresses

We are going to geocode language information from a spreadsheet. This data was collected from various sources, and may be similar to the type of data you will be collecting in your projects. We will use the Geocoder provided by the [US Census](https://www.census.gov/geo/maps-data/data/geocoder.html). Carto will geocode up to 100 points for free.

1. Go to the [data folder], and find the ColumbiaLanguages.csv file and save it to your computer (click 'View Raw'. If you are on a Mac, click `Command + s` to save it. On a PC, select it all and save it to a Text Document (in Notepad, Text Wrangler, or Sublime)).
2. Go to the 'DataView' and select 'Add New Dataset'. Add the 'ColumbiaLanguages.csv'. Return to the Dashboard/Home
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
	1. Open GeocodeResults.csv in Excel (This can also be done in Google Sheets)
	2. You may notice that the language and department data is missing. Don't worry about that yet, we will come back to it.
	3. Select the column that looks like Latitude, Longitude numbers (probably Column F)
	4. Insert a Column to the Right
	4. On the Data Tab, select Text to Columns
	![txtcol](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/latlongtxtcol.png)
	5. Select 'Delimited' and 'Comma' as prompted
	6. Rename your columns Latitude and Longitude (Latitude = 40.xxx)
	6. Save this file
	7. Optional: I prefer to remove columns that I won't be using before I enter it into Carto:
		1. If they are all a 'Match', remove 'Matching Result 1.' If they are not all a 'Match', inspect the ones that are not and then remove the column. 
		2. If they are all 'Exact', remove 'Matching Result 2' Inspect any fields that are not 'Exact' before removing the column.
		3. The first address column. If everything is an 'Exact Match', the second address column is redundant. If they are not an 'Exact Match', the second address column is the address used to obtain latitude and longitude. You likely want to keep both columns in this case. 
		4. Save the new, clean file
7. Return to the Carto home, and switch to Datasets View. Select 'Add New Dataset' and upload the GeocodeResults.csv that you just cleaned.

8. Select 'Create Map'
	1. You should see a map of New York with some light orange dots on it. 
	![dots](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/corange.png)
	
10. At this point, these are just points without any information attached. We need to add the language information that we have in the ColumbiaLanguages.csv file.
	1. Return to the Layers View
	2. Select 'ADD ANALYSIS'
	![add analysis](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddanalysis.png)
	2. Select 'Join Columnbs by second layer'
	3. Connect the `ColumbiaLanguages.csv` dataset
	4. Join on the 'id' field for both files.
	5. Make sure you select the 'id' field for at least one of the datasets so you have a link back to the originals.
	6. Be sure in the Columbialanguages dataset you select description, address, name, etc. 
	7. Export this dataset as a csv file.
	![export](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cexportdata.png)
11. We will use the exported file to create a new layer.


## Part III - Representing this data

Because there is no statistical or numerical data associated with this map, the best way to represent this data is either simple points or clusters. Simple points allow you to turn on the click or hover feature where you can display information about each point. Clusters represent how many lines are represented at each location. 

If you choose to display the data and want to have each point displayed, but slightly askew from each other so that it appears that they are in slightly different locations in the same building, you may have to manually manipulate the data.
	1. Upload the file you just downloaded again as a new layer
	![add layer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddlayer.png)
	2. You may want to rename it 'ColumbiaLanguages' using the 3 dots to keep organized.
	3. Click on this layer to go to the Data View.
	![add layer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cdataview.png)
	4. Select 'Analysis'
	5. Add popups with the name of the office and the name of the language.
	6. Change the label name to make it clearer for your user
	![add layer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cpopup.png)
	
## Part IV - Simple Style
You can do a LOT in this new version of Carto to style your map and help tell the story. 
	1. These orange dots are awfully small. Let's change them
		1. Under 'Style' click on the Number (7), and make it larger, like 15
		![changesize](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cfixval.png)
		2. Change the color if you wish by clicking on the Orange bar
	2. This is looking better, but we are seeing both layers at once (eventhough our bigger dots are covering the smaller). Let's fix that.
		1. Return to the layers panel
		2. Click on the eye icon next to layer 'A', the base geometry. This will make it invisible.
		![changeviz](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/ceye.png)
	1. Change the basemap (I chose watercolor) 
	![watercolor](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cwater.png)
	2. You can use custom maps or tiles from other servers.


## Part IV - Exporting the Map for use in the Case Study

1. Click on Share
	1. Select your Privacy settings
	2. Select 'Publish'
	3. Select the 'Embed' option
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
2. Go to the Dataset View and select 'New Dataset'
3. Upload the map.osm file from your computer
4. If you have an option, it is the **POINTS** file
4. Return to the DataView and inspect this new dataset. 
5. Switch to map view to get a sense of what information is positioned where. 

There is a lot of information here. We are not interested in all of it. Let's look only at the Bicycle Parking. We can image a project where we want to know if speakers of a language have access to bike parking (hospitals, groceries, etc.).

1. Go to the Data View of this layer
1. Open the `SQL` Editor with the slider at the bottom
![sqlosm](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/csql.png)
2. If you forget what features/columns are available to you, click on the icon with 3 veritcal bars on the lower right hand side.
![dataview](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cdata.png)
2. We want to SELECT everything FROM the dataset, map_points, WHERE elements in the column, 'other_tags' is LIKE "amenity"=>"bicycle_parking" 
![sqlselect](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/csql.png)
	1. SELECT * FROM mmcsweeney.map1_points WHERE other_tags LIKE '%"amenity"=>"bicycle_parking"%'
		1. The name of the points file will be your user name
	2. '[LIKE](https://www.postgresql.org/docs/8.3/static/functions-matching.html)' means that the target string is in the entire string. 
	3. The % % on either end are a [Regular Expression](http://www.regular-expressions.info/). They mean 'Wildcard', so anything can come before or after the target string.
	![sql](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/csqlout.png)
	4. Apply the Query and return to the map view.

Congratulations! You have now uploaded OSM data into a Carto Map. You can, of course, do much more with this (i.e., concentration of cafes versus [candy store](http://gothamist.com/2014/05/02/ask_a_native_new_yorker_whats_the_d.php) ('bodega','deli', 'corner grocery', etc.) in a given language neighborhood, etc. 



