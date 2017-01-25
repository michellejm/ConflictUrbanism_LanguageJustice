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

You will need to set up a (free) account on [Carto](www.carto.com) (formerly CartoDB).

### Spatial Data and Boundaries

We are going to be working with Census Data about income and language in New York City. First we need to decide what kind of boundaries we are going to use.  There are 5 ways spatial data is divided in New York City (block groups, census tracts, neighborhoods, PUMAs, and counties). 

* Block groups are just as they suggest, a group of blocks, there are approx. 6,500 in New York City. Because they are so small, they can have a large margin of error.  
* A census tract is approximately 4,000 people, there are more than 2,000 in New York City. They also tend to have a high margin of error, but not to the level of block groups. 
* Neighborhood Tabulation Areas (NTAs) are a unit created by the NYC Department of City Planning in order to display data in a more meaningful way to those very familiar with New York City. They are created through simple addition of census tracts. 
* PUMAs (Public Use Microdata Areas) are used by the Census (not just in NYC), and are areas of approximately 100,000 individuals, also tabulated by adding together block groups.
* Counties (a legal subdivision of the state) are also used by the Census and in New York City, correspond to the boroughs (Brooklyn = Kings, The Bronx = Bronx, Manhattan = New York, Queens = Queens, Staten Island = Richmond). 

The dataset we will use comes from the [American Community Survey](https://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml). For more on finding and cleaning datasets, see [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md). The American Community Survey is sent to a sample of households every year. It is meant to supplement the dicennial census. Data is available yearly or in 3-5 year estimates. Because language data can tend to be small percentages, it is better to use 5 year estimates to get a more accurate representation of the languages spoken in a neighborhood.

Language data from the census comes in many forms. We will use Language by ability to speak English for the population age 5 and over. The census makes a distinction between those who speak English 'very well' or 'less than very well'. Regardless if this information is relevant to your project, it is what you will receive. The raw numbers and their margin of error as well as a text description file are usually bundled together.

## Part II - Uploading Data

The data we are using for this tutorial has already been cleaned for our purposes.  Carto comes pre-packaged with a basemap that represents the Earth, with many features already represented (i.e., water, country boundaries, etc.). The default map projection is Web Mercator. Web Mercator is used because it is efficient, not because it is visually accurate. Web Mercator is good enough for our purposes since we will be looking at very small areas, so the visual distortion is not as significant. If you want to be more accurate or represent an area larger than the US, check out [this blog post](https://carto.com/blog/free-your-maps-web-mercator) on how to change the projection in Carto. Shapefiles are projection-independent, so you can use any shapefile with any projection. 

We need to upload a shapefile that has the boundaries we want to impose on our map, we will essentially be cuttng up New York City into smaller units. We know something about the languages represented in that smaller area. 

1. Import a shapefile of census tracts for New York City. This file came from [the US Census](https://www.census.gov/geo/maps-data/data/cbf/cbf_tracts.html), though it is available from many sources.

	1. Go to the [data folder](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/tree/master/Data)
	2. Find `gz_2010_36.csv` and download it to your computer (click 'View Raw'. If you are on a Mac, click `Command` + `s` to save it. On a PC, select it all and save it to a Text Document (in Notepad, Text Wrangler, or Sublime)).
	3. Return to Carto >> Add Dataset
	4. Upload the file here
	5. Carto will show you the map view. It should look like New York City divided into census tracts.
	6. Return to Data View (with the slider at the top)
	![dataview](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/dataview.png)
	7. For clarity, I'm going to edit the metadata and rename my dataset "nyc_censustracts"
	![freemeta](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/metadata.png)

2. Add data from a csv (comma separated values) file.  We are going to add language-speaker data to the census tracts. The data came from [National Historical GIS](https://www.nhgis.org/) by submitting a data request. This is an excellent location to find all kinds of census data, especially when working with datasets from multiple time periods. It has been pre-cleaned for this tutorial. For more on data cleaning visit [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md).

	1. Go to the [data folder](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/tree/master/Carto/Data) on the Github Page.
	2. Find "nhgis_language_percents_nyc.csv" and download it to your computer.
	3. Add this dataset to your 'My Datasets' Library
	![datasets](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/cartodataset.png)
	4. Notice the Column named 'GISJOIN' this is the column we are going to use to merge those two datasets. Look back at the census tract file. It also has a GISJOIN column. These numbers correspond to each census tract.
	5. Return to Carto and navigate back to the DataSets Page (*small arrow in left hand corner*)
	6. Upload the "nhgis_language_percents_nyc.csv" 
	7. It will not automatically show you a map view, so click on the slider to see the map view.
	8. It should ask you to Georeference the dataset. DO NOT GEOREFERENCE IT! There is no geographic information in this dataset - only statistical information.
	9. Return to DataSets
	
3. Combine Files - Now we are going to align the language information to the census tracts.
	1. Open the "NYS_censustracts" dataset
	2. Merge this dataset with another (Click Edit >> Merge with dataset) *This will create a new dataset*
	3. Select 'Column Join'
	4. Find the 'nhgis_language_percents_nyc' file
	5. Select 'cnty_tract' for both files, and click 'Next'
	6. All of the languages and county names should be selected. If they aren't, select them now.
	7. A new dataset will appear. I'm going to rename mine, "languages_by_censustract_nyc"
	8. Carto will probably suggest some "interesting maps" ignore these.
	
## Part III - Mapping data
In this section, we will look at the data in a map form. At this point, our questions are exploratory.

1. Make the data into a map
	1. In the upper right hand corner, click on 'Visualize'
	2. Carto will prompt you to make a map. Accept this.
	3. This changes your dataset from a spreadsheet with a spatial component into a map you can add layers to within the system.
	
2. Inspect the data
	1. Click on the number '1' in the box on the right side of the screen. This is the first layer. 
	2. If it isn't selected already, click on the little square with a paintbrush. This is the mapping 'wizard'. Eventually, you will create these maps manually, but for right now, let's just look at the built-in options.
	3. Select Choropleth. Choropleth maps are good for showing differences in density. Our language data is perfectly suited to this.
	4. Select any language. I'm going to choose Chinese.
	5. Does this align with what you might expect for the city? Why or why not?
	
3. Add a Tooltip
	1. Click on the 'infowindow' box directly below the 'wizard' box.
	2. There are two options here - 'click' and 'hover' - pick your preference.
	3. Select a language to show, I'm choosing Chinese since we're looking at the Chinese map.
	4. Go back to the map and either click or hover over one of the census tracts, two numbers should appear. 
		1. The decimal represents the percentage of speakers
		2. The grey number represents the row where that datum appears in the table (only visible to you)

4. Formatting the Tooltip
*We want the tooltip to display as a percentage, not as a decimal. We can do this one of two ways. First, we could reformat the data in Excel, to natively be a percentage. Second, we can do it using SQL commands. I am going to chose the SQL commands because it gives me more control over the data.*
	1. Click on the icon that says 'SQL' (directly above the wizard)
	![sql](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/sql.png)

		1. SQL is a very old computer language still used for databases. Carto is treating your dataset as a database, and querying it for information. 
	3. We are going to change the query.
		1. Currently, it should say: **SELECT \* FROM languages_by_census_tracts_nyc** This means *select everything from the dataset, languages...* For this layer, Carto has access to all the information on your dataset. This layer is about Chinese, so we will restrict it to just Chinese.
		2. Remove the original command and replace it with: **SELECT \*, to_char(chinese, '99V99%') AS chinese_percent FROM languages_by_census_tracts_nyc** *This says select everything from the dataset, languages..., and change the characters in the chinese column to a percent formal and call that transformation chinese_percent
		3. Run this query by clicking 'Apply Query'
	4. Now return to the tooltip and select the new variable, chinese_percent (and deselect the old chinese).
		
5. Making layers
	1. In the last step, we make layer 1 for Chinese. Let's make another layer for Arabic.
	2. Click on 'Add Layer', directly above the Chinese layer
	3. We are going to do the same for Arabic that we did for Chinese.
	4. Select Choropleth Map view (Step 2)
	5. Apply the SQL filter for Arabic (Step 4)
	6. Add the tooltip (Step 3)
	7. Be sure to rename the layer
	8. Repeat for as many languages as you want

6. Customizing Views
	1. Toggle the visibility of layers by selecting the layer and moving the slider button on the top right hand side of the title bar.
	2. Add a layer selector to your map by changing the settings
		1. On the map, in the lower left corner is the 'Options' button.
		2. Select 'Layer Selector'
		3. Selection now appears in the upper right side of the map
	3. Add a title and a legend in the 'Add Elements' box.
	
Congratulations! You have made your first map!! 

7. You are welcome to change the colors, highlight different languages, change the basemap, etc. This is not required.

To complete this tutorial, send your finished map to Michelle at mam2518@columbia.edu

1. Select `Visualize`
![visualize](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/visual.png)
2. Accept to create your map.
3. Select 'Publish' and send me the link.
 
	
To learn how to do more with Carto, work through the [Carto 2 Tutorial](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_2_Carto_Part2.md) or visit the [Carto Tutorials](https://carto.com/docs/tutorials) page.

	
