# Rasters and Historical Maps with QGIS - Part II

The purpose of this tutorial is to introduce you to mapping using rasters. By the end of this tutorial, you will be able to:

1. Determine if your project will require rasters or vectors or both.
2. Combine raster and vector data in the same project.
2. Create a raster file from a vector file.
3. Find and import georeferenced historical maps into your project.
4. Calculate population change in an area through raster layers.


## Background
Raster data is primarily used in 3 ways:
* Basemaps (i.e., a georeferenced historical map with contemporary infomation overlaid)
* Surface maps (i.e., population density, rainfall, or temperature)
* Thematic maps (i.e., land use maps)

Raster data is essentially a matrix of pixels (cells) each with a given value. So far, we have focused exclusively on vector data. Vectors consist of points, lines, polygons. Vector data is useful when you have information about an area and want to ask questions about it in relationship to other information about an area. The geometries don't have to be the same (i.e., asking questions that reference data about both points and polygons as in the [QGIS 1](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_3_QGIS1.md) Tutorial). 

Rasters, on the other hand, represent spatial information through pixels. Imagine that the entire surface of the Earth is covered in a grid. Raster data gives each cell in that grid a value (cells "without" a value get 0). So, rather than drawing the boundaries (i.e., census tracts, counties, etc.), we think of the entire area as one unit, divided by pixels. The first layer of pixels determines some attribute about the space. The second layer, another attribute, etc. Calculations can be performed between the layers. The difference between regular images (pictures, historical maps) and raster files is that raster files have geographic information associated with them. So though they are both created through a matrix of pixels with different values, rasters are aligned to spatial information (and correspondingly, have a CRS or projection associated with them). 

In this tutorial, we will go over two ways to use rasters. In the first, we will use georeferenced historical maps as basemaps, essentially combining raster and vector data. In the second, we will use two raster layers to analyze population change. 

## Getting Started
Download the GitHub repository for the tutorials. Using the green button [here](https://github.com/michellejm/ConflictUrbanism_LanguageJustice), select `Download ZIP`. The Data folder has all of the files needed for this tutorial. If you do not have QGIS installed on your computer, [install it now](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Install-QGIS.md).

The data for this tutorial came from:
* American Community Survey 5-Year Estimates 2011-2015 (Table B16002)
* American Community Survey 5-Year Estimates 2006-2010 (Table B16001)

The boundary files came from:
* [NYC Planning Department](http://www1.nyc.gov/site/planning/data-maps/open-data/districts-download-metadata.page) for the Census tracts clipped to shoreline
* [NYC Planning Department](https://www1.nyc.gov/site/planning/data-maps/open-data/dwn-nynta.page) for neighborhood tabulation areas

The Georeferened historical map comes from:
* [NYPL Map Warper](http://maps.nypl.org/warper/maps/27259#Export_tab)


First, we are going to take a vector file and turn it into a raster file. 
1. Open QGIS 
2. Add a vector layer
![vector](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/vectorlayer.png)
3. Add the `NYCT-Langs_ACS5YR_2015` Shape file from the Data>Q2 folder.
  * This file was created by joining census data to the 2010 census tracts that have been clipped to the shoreline (nyct2010_16d). The data wsa cleaned and modified to allow a column join. The values were then transformed from integers to real decimals with a precision of 2. For more on data cleaning, see [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md)
4. This file will appear as census tracts for New York City. 
![tracts](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2addvect.png)
5. Right click (or Control+Click) on the layer name to Open Attribute Table. You should see metadata, information about the geometries, and Languages at the far right. Name that begin with 'O' refer to 'other' of that group. If everything looks ok, close the Attribute table
6. Now we want to add the Neighbohood Tabulation Areas Shapefile as a Vector Layer. It should be in Data > nynta
7. Change the fill of the nta file to 'Transparent' (Double click the layer name > Style> Simple Fill > Transparent)


## Make a Population Density Map
1. In the Map View again, select Vector > Research Tools > Random Dots
 * Input Boundary Layer: NYCT-Langs_ACS_5YR_2015
 * Use value from input field: Arabic
 * Add result to canvas (YES)
 * Output Shapefile: ArabicDots (saved where ever makes sense to you)
 * OK
 * Close
2. Change the Style of the dots so they are 1 PIXEL (Double click the layer name > Style > Simple Marker > Change 'Size' and 'Border' (Change 'Color' if you need/want to)
3. Deselect the layer with the tracts 'NYCT-Langs_ACS_5YR_15'
4. You should now see 1 dot representing every Arabic speaker in NYC overlaid on the neighborhood boundaries. 

### Transform a Vector into a Raster
**STOP!!!** This is a point where Projections become very important. Take a minute to look a the projection you are using. The projection for the project is in the bottom right hand corner. 
![project](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/projection.png)
What projection you want to use could be the topic for an entire class. We will use Web Mecator because we plan to use our map as a webmap, and Web Mercator is the standard projection for Web Maps. 

**Change your projection**

1. Click on the CRS number 
2. Select 'Enable on the fly transformations' at the top of the page
3. Select 'WGS 84 / Pseudo Mercator EPSG 3857'
4. Double Click on your NYCT-Langs_ACS_5YR_15 layer to be sure that it is ALSO in Psuedo Mercator (it's under 'General')
5. If it is not, fix it now (since we turned the layer off when we changed the projection, it didn't change with the rest of the project). 

**Now Transform the data**
1. Select Raster > Conversions > Rasterize (Vector-to-Raster)
![rasterize](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2rasterize.png)
2. Select your parameters
 * Input file: NYCT-Langs_ACS_5YR_15
 * Attribute Field: Arabic
 * Output file: Arabic15Raster (GeoTiff is the default - keep this)
 * Raster size in pixels (3000 x 3000)
 * Load into canvas when finished YES
 * OK
 * Close
3. Nothing changed, now what?
4. Save your project.
5. If your Arabic15Raster.tiff file exists (where you saved it), you have made a raster file!
6. Save your Project!!

## Calculate Population Change
1. Open a new Project
2. Import the Arabic15Raster file we just created.
3. Import the Arabic10Raster file from the Data folder. This file was created in the same way as Arabic15Raster. The supporting data for the other languages is in the Q2 Data folder.
4. Both of these raster files are in the 'WGS 84 / Pseudo Mercator EPSG 3857' Projection. Make sure that both of the layers and the project are in this CRS. If they are not, change them now.
5. This is difficult to look at because the colors are inverted (white indicates high density, black indicates low). We want to change this for both layers. 
  1. Double click on the layer. 
  2. Select Style and change the Color Gradient to 'White to Black'.
  ![raster style](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2raststyle.png)
6. Now we want to calculate the difference between these two layers.
  1. Select Raster > Raster Calculator
  ![raster](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2rastc.png)
  2. Double click on each layer to add it to your equation. We want to subtract the 2015 data from the 2010 data and add it to our map.
  ![rastcalc](![raster style](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2rastcalc.png)
  3. Save your new layer as Arabic_Diff_2010-2015
  4. Select Add to Map
  5. A new layer should appear with a grey background. 
7. Style this map to illustrate what we want to know.
  1. Deselect the original two Arabic layers so only the Arabic_Diff layer is showing.
  2. Double click to open the Properties Window
  3. Change the Render type to Singleband pseudocolor
  4. Change the color scale to be multicolored (I'm choosing BrBG to symbolize loss of speakers (Brown) and growth (Green)).
  5. Click on 'Classify' to appy your changes. The value ranges appear at the left. 
  6. Note that the white color in the middle is not 0. We, as viewers, would expect no change to be colorless. Double click on the number to change this value to zero and click Apply (QGIS took the midpoint of the data, since there was an overall gain in Arabic speakers, the midpoint is slightly positive).
  ![raster style](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2grad.png)
8. If this map makes you a little disoriented, add the Neighborhood Tabulation Areas vector layer, and change the fill to transparent. 

Another approach we could have taken was to add the layer together to symbolize the neighborhoods with the most speakers over the past 10 years, or taken data over many years to determine which are the most established neighborhoods. We could also use this type of map to visualize what languages are moving out of a neighborhood and what languages are moving in. 

**Export your map as a .jpeg** and send it to Michelle at mam2518@columbia.edu(do not use Composer - we have another map to make).

## Use a Historical Map

What if we want to illustrate modern information on a historic map? For example, I want to know what features were present in an area before a given group moved into that area. One way we could do this is layering raster data for every five years on a base map and visualizing the progression as layers. 

Historical maps start out as images and then get "georectified" to align to modern maps in modern projections. The NYPL has made public thousands of historical maps via their digital map collection. Even better, many of these are already georectified! The [NYPL Map Warper](http://maps.nypl.org/warper/) is an crowd-sourced project to rectify historical maps and align them to modern ones. You can download the georeferenced raster files to use in your project, you can use them data, as base layers in webmaps, or download them strictly as images. 

In this tutorial, we are going to layer modern information about Russian speakers in New York City to a historical map of Brooklyn. We know that Russians began arriving in New york City around 1905, and there are strong Russian speaking enclaves throughout the city today. A more complete project would also incorporate the 1920 Census data and the 1980 and 1990 census data as layers on this map. 

1. Visit the NYPL Map Warper site and Export [map 27204](http://maps.nypl.org/warper/maps/27204#Export_tab) as a Warped GeoTiff. Two files will be downloaded. These must stay together in the same folder. 
2. Start a new Project in QGIS
2. Add two Raster Layers
 3. Add the Russian1910.tiff Raster layer
 4. Add the 27204.tiff Raster file you just downloaded
3. Move the Russian speaker data on top of the NYPL Map
![raster](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2rasts.png)
4. Double click on the Russian Speaker data layer to change the style of the map
 1. Style > Color gradient >> white to black
 2. I like to do, but it's not necessary: Style > Blending Mode > overlay
 2. Transparency > 50%
5. Drag the 'Zoom In' magnifying glass over Coney Island/Sheepshead Bay (lower Brooklyn) to narrow in on this area. 
6. The Data Folder also contains a Russian15.tiff file that has the census data for Russian speakers for 2015 if you would like to add that layer for comparison. 
7. We will learn how to use leaflet to add layers to a webmap in [Tutorial 7](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_7_Leaflet.md). 


To complete this tutorial, export this map (either Export As Image or use the Print Composer)
![raster](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/q2prints.png)
and email it to Michelle at mam2518@columbia.edu.


Congratulations!! You have completed the Final Mapping Tutorial for the Conflict Urbanism: Language Justice Course. There are, of course, many more topics to cover that will help support you mapping project, but as of now, you should have enough familiarity with mapping to be able to make a map to support your final project. 

____________________
This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered as part of the Mellon Grant for Architecture in the Humanities in the Center for Spatial Research. 

