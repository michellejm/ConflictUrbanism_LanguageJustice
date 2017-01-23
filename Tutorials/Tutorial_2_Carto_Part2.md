# Carto Tutorial - Adding points to Carto

By the end of this tutorial, you will be able to:

* Add points to a basemap manually and from a spreadsheet.
* Geocode a group of addresses.
* Make decisions about how to display information on your map.
* Import data from Open Street Map into your own map.



The assumption in this tutorial is that you have collected raw data from the world and want to represent where that data exists. There are a lot of things to do with that data, including labeling it in a creative, provocative, or alternative way, geocoding it to find latitude and longitude, aligning it to other information about the physical or social space it inhabits. 

First thing, we have to get that data onto the map. Though there are many ways to represent shapes on a map, we are going to start with latitude and longitude. Determining the latitude/longitude of a point is referred to as "geocoding." Addresses, points, intersections, events, etc. can all be geocoded and therefore represented as latitude and longitude.  Carto does this automatically when you place a point on a map. 

## Part I - Adding individual points

1. Go to the Carto Dashboard and click on 'New Map' in the upper right hand corner.
2. You will arrive on a page to add datasets. Click on 'Create Empty Map' on the right side of the page.
3. You will be prompted to add 'Points', 'Lines', or 'Polygons'. Select 'Point'
	1. Alternatively, click on the little bubble in the lower right hand corner
4. In this tutorial, we are going to map language information about Columbia University. For each combination, drop a pin on the building (if you don't know the shape of the building, just drop a point somewhere on campus. Toggle to DataView to add the relevant information about the pin. In DataView, double click on the box you expect it to go in.
	1. Schermerhorn Extension, Center for Spatial Research, English
	2. Butler Library, Ancient & Medieval Studies Reading Room, Ancient Greek
	3. International Affairs Building, Language Resource Center, Yoruba
5. Latitude and Longitude should appear for each of these locations. Clearly this is a tedious way of making a map. 

## Part II - Geocoding batches of addresses

We are going to geocode language information from a spreadsheet. This data was collected from various sources, and may be similar to the type of data you will be collecting in your projects. We will use the Geocoder provided by the [US Census](https://www.census.gov/geo/maps-data/data/geocoder.html). Carto will geocode up to 100 points for free.

1.  Download the zip file from the Carto_2 Repository, and find the ColumbiaLanguages.csv file. This file is already formatted for you. To use the Census Geocoder, the file must be in .csv format, and include the following information:
	1. Unique ID,
    2. House Number and Street Name,
    3. City,
    4. State,
    5. ZIP Code
2. Visit [Census Geocoder](https://geocoding.geo.census.gov/geocoder/)
3. Select Find Locations Using... Address Batch
4. Upload the ColumbiaLanguages.csv file
5. A csv file will be returned with the following information: IMAGE HERE.
6. To use this file in Carto, we have to clean it. 
	1. Open GeocodeResults.csv in Excel
	2. You may notice that the language and department data is missing. Don't worry about that yet, we will come back to it.
	3. Select the column that looks like Latitude, Longitude numbers (probably Column F)
	4. On the Data Tab, select Text to Columns IMAGE HERE 
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
	1. Click 'Edit' and 'Georeference Layer'
	2. You will be prompted to select which column has Longitude and which has Latitude.
	3. Return to Map View and zoom in on Columbia, you should see your points
10. At this point, these are just points without any information attached. We need to add the language information that we have in the ColumbiaLanguages.csv file.
	1. Return to your Carto Dashboard, and find 'Your Datasets'
	2. Add a 'New Dataset'
	3. Connect the ColumbiaLanguages.csv dataset
	4. Once it appears in the DataView, select 'Edit' and 'Merge with Dataset'
	5. Merge it with the GeocodeResults dataset, and join on the 'ID' column
	6. Once the datasets are merged, go to the MapView
11. Now the information about each language and department is attached to the markers. 

##Part III - Representing this data

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







