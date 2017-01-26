# Carto Tutorial 1 - Getting Started on Carto

By the end of this tutorial you will be able to:

1. Describe where geographic data comes from
1. Make a decision about geographic boundaries
2. Upload a dataset into Carto
3. Join two datasets based on a shared feature.
4. Explore the resulting dataset through a map
5. Add layers to your map
6. Export your map 

## Part I - Getting Set Up

### Account

You will need to set up a (free) account on Carto (formerly CartoDB). Columbia Libaries has a subscription to an enterprise version of Carto available [here](http://library.columbia.edu/locations/dssc/technology/gis.html) with your Columbia University email. The interface has recently dramatically changed. If you have the older version of Carto, please work through [this tutorial](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Old/Carto2016_part1.md).

### Spatial Data and Boundaries

We are going to be working with Census Data about income and language in New York City. First we need to decide what kind of boundaries we are going to use.  There are 5 ways spatial data is divided in New York City (block groups, census tracts, neighborhoods, PUMAs, and counties). 

* Block groups are just as they suggest, a group of blocks, there are approx. 6,500 in New York City. Because they are so small, they can have a large margin of error.  
* A census tract is approximately 4,000 people, there are more than 2,000 in New York City. They also tend to have a high margin of error, but not to the level of block groups. 
* Neighborhood Tabulation Areas (NTAs) are a unit created by the NYC Department of City Planning in order to display data in a more meaningful way to those very familiar with New York City. They are created through simple addition of census tracts. 
* PUMAs (Public Use Microdata Areas) are used by the Census (not just in NYC), and are areas of approximately 100,000 individuals, also tabulated by adding together block groups.
* Counties (a legal subdivision of the state) are also used by the Census and in New York City, correspond to the boroughs (Brooklyn = Kings, The Bronx = Bronx, Manhattan = New York, Queens = Queens, Staten Island = Richmond). 

The dataset we will use comes from the [American Community Survey](https://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml). For more on finding and cleaning datasets, see [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md). The American Community Survey is sent to a sample of households every year. It is meant to supplement the dicennial census. Because language data can be small, it is better to use 3-5 year estimates to get a more reliable representation of the languages spoken in a neighborhood.

Language data from the census comes in many forms. We will use 'Language by ability to speak English for the population 5 years and over'. The raw numbers and their margin of error as well as a text description file are usually bundled together.

## Part II - Uploading Data

The data we are using for this tutorial has already been cleaned for our purposes. 
Carto comes pre-packaged with a basemap that represents the Earth, with many features already represented (i.e., water, country boundaries, etc.). The default map projection is Web Mercator. Web Mercator is used because it is efficient, not because it is visually accurate. Web Mercator is good enough for our purposes since we will be looking at very small areas. 
If you want to be more accurate or represent an area larger than just a city, check out [this blog post](https://carto.com/blog/free-your-maps-web-mercator) on how to change the projection in Carto. 
Shapefiles are projection-independent, so you can use any shapefile with any projection. 

Our first layer is our **geometry**.
We need to upload a file that has the boundaries we want to impose on our map, we will essentially be cuttng up New York City into smaller units (census tracts). 

1. Import the csv file of of census tracts for New York City. This file was modified from [NYC Open Data](https://data.cityofnewyork.us/City-Government/2010-Census-Tracts/fxpq-c8ku), though it is available from many sources. This is the NYC Open Data Interface. The file we will use has been modified to make this tutorial more straightforward. We will work more with preparing data in [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md)
![downloadfile](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cdownload.png)


	1. Go to the [data folder](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/tree/master/Data/Carto)
	2. Find `gz_2010_36.csv` and download it to your computer 
	
		1. Click `View Raw`. If you are on a Mac, click `Command` + `s` to save it. On a PC, select it all and save it to a Text Document (in Notepad, Text Wrangler, or Sublime).
		2. You *may* have to change the file type. By default, it will probably offer 'HTML' or 'Web Archive', change it to 'Text' or '.txt', or 'Page Source' depending on yur computer and browser.
		3. If propted to Append '.txt' to the name, select 'Don't Append'
		
	3. Return to Carto >> Add Dataset
	![addset](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cdatasets.png)
	
	4. Upload the file (Browse or Drag/Drop)
	5. Carto will show you the data view. This is just a list of Polygons. 
	6. Select 'Create Map' in the lower right corner. It should look like New York City divided into census tracts.
	![create](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/ccreatemap.png)
	7. It should look like New York City divided into census tracts.
	![basemap](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cbase.png)
	8. For clarity, I'm going to edit the rename my dataset "nyc_censustracts"
	![freemeta](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cmeta.png)

2. Now we want to add language data to the map. 

3. We will add language data from a csv (comma separated values) file. The data come from [National Historical GIS](https://www.nhgis.org/) by submitting a data request. This is an excellent location to find census data, especially when working with datasets from multiple time periods. It has been pre-cleaned for this tutorial. For more on data cleaning visit [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md).

	1. Go to the [data folder](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/tree/master/Data/Carto) on the Github Page.
	2. Find "nhgis_language_percents_nyc.csv" and download it to your computer.
	3. Return to Carto, and select 'ADD'
	![addlayer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddlayer.png)
	4. Connect the language percentages in New York City dataset
	![connect](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cconnectdata.png)
	5. Select 'Add Layer' in the lower right corner.
	6. Carto will return you to the map view. 
	7. Both of your layers should now appear (A and B)
	8. On the 'nyc_census_layer' (Layer A) Select 'Add Analysis'
	![addanalysis](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddanalysis.png)
	9. Select 'Join columns from 2nd layer'
	10. Input #1 should be your census file
	11. Select your language file for Input #2
	12. Join type is 'Inner'
	13. For the Foreign Keys, select 'Cnty_tract' for BOTH files
	14. Select the Columns you want to keep on each file. 
		1. Be sure to select cnty_tract on at least one of them (to maintain a link to you original data).
		2. Select all of the languages you are interested in. 
	15. Select Apply.
	16. Your map should still be solid blue. 

4. Now we want to see what this data looks like on our map. We are going to make a chloropleth map based on speaker density in census tracts. Chloropleth works best to represent density. Bubbles of various sizes work best to represent raw numbers. 
	1. From the Analysis Panel, select 'Style'
	![addstyle](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cstyle.png)
	2. Click on the Fill (blue bar) and Select 'By Value'. Pick your language (for this, you might want to pick something that you know there are a community of speaker (i.e., Greek or Korean are good choices, Navajo might	 not give you enough data for this type of map).
	3. A chloropleth map of that language should appear. 
	![addchloro](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cchloro.png)
	4. This is great, but we probably want to have popups to tell us more information about the number of speakers. 
	5. Next to the style button is 'Pop-Ups'. You can choose from Hover or Click, and Include any information you want. (Hover might not work in the prview mode)

NOTE: The information being displayed i sjust being pulled in form the spreasheet. You can edit it, add information or relabel rows based on what you want to highlight (i.e., your label can make a claim or commentary on the tract).

OK, what if we want to creat multiple layers? I.e., I want my user to be able to view Chinese, Korean, or Vietnamese neighborhoods by selecting layers on my final map. 
The most efficient way to do this is to export the joined data table we created and create a new map with it. Then add that table with different language columns highlighted. 
	
1. Export the data (the layer that has the Join in it) by clicking on the 3 little dots and 'Export Data'
![export](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cexportdata.png)
2. Download as CSV and remember where you save it to.
3. Return to Home Screen (by clicking the small white circle on left)
![dataview](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/chome.png)
4. Upload this file you just downloaded as a new dataset. Let's take a shortcut. 
	1. Select 'New Map' on the Right side
	2. Select 'Connect Dataset'
	![connect](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cconnectdata.png)
	3. This will take you to a map where the joined layer is the baselayer.
5. Change the name of the map by clicking on the 3 little dots next to 'Untitled Map'. I'm going to change it to NYC Languages.
6. The imported layer will be the first layer. 
	1. Select 'ADD ANALYSIS' again
	![addanalysis](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddanalysis.png)
	2. Select 'Filter By Column Value'
		1. In the 'Filter by column value' Category
			1. Input = the table you just uploaded
			2. Column = 'English only' OR the column with the language you are interested in (it might say 'right_LANGUAGE', that's fine.)
		2. In the 'Parameters' Category
			1. Filter = Is Greater Than
			2. Value = 0 (this could be something like .05, if you are looking for concentrations of speakers.
		3. 'APPLY'
	3. You should see another solid colored map. Go to 'Style' and change it to a Chloropleth again.
		1. Select the language you filtered by (i.e., English only)
	4. Change the name of the layer based on the language (select the 3 little dots next to the dataset name and 'Rename')
	5. Change the legend by selecting 'Legend' (next to PopUps). The data in this files does not follow capitalization rules. 
	5. OPTIONAL: Add tooltips or Widgets
		1. On the Data Tab at the Left, there is the option to add 'Widgets'. These add graphs to your map.
			1. Select the Only English (or other language) - it will add a graph of how many census tracts are in each percentage group.
			2. Select the little drop icon to have the census tracts and the graph colors match. 
			3. You can customize the graph type or the colors by selecting the 3 dots icon and making your choices on the left. 
6. Add a second layer. 
	1. Select the Left Arrow until you arrive at the layers page. You may have to select the Layers tab.
	![left](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cleftarrow.png)
	![layers](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/clayers.png)
	2. Select 'Add'. You will be directed back to the datasets. Add the same censustracts+languages dataset
	![addlayer](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/caddlayer.png)
	3. It will be imported as layer 'B'. 
	4. Repeat Step 6, starting with 'ADD ANALYSIS'
		1. Filter By Column Value
		2. Pick another language (i.e., Chinese)
		3. Repeat
7. Add a third layer following the same steps.
8. You can change the order of the Layers by dragging them by the small keys ar the left. This will change the order that viewers can see them. In this case, it doesn't matter in terms of the map since all the layers are opaque. It does mean that only the top layer will be viewable when the user arrives at your map. We need to provide them the option to see other layers. 

9. Add a layer selector to your map. 
	1. Click on the Map Options icon
	![options](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cselector.png)
	2. Select the layer selector option. 

10. Share your map (you can still edit it)
	1. Select the 'Share' button in the lower right corner
	2. Click on the 'Private' button and choose 'Only with Link'
	3. Click on the 'Publish' button
	![share](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cprivate.png)
	4. Change to the 'Publish Tab'
	5. Copy the link
	
	
Congratulations! You have made your first map!! 

To complete this tutorial, send the link to your finished map to Michelle at mam2518@columbia.edu

	
To learn how to do more with Carto, work through the [Carto 2 Tutorial](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_2_Carto_Part2.md) or visit the [Carto Tutorials](https://carto.com/docs/tutorials) page.

	
