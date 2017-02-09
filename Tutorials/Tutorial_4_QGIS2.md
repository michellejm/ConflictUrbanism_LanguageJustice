# Rasters and Historical Maps with QGIS - Part II

The purpose of this tutorial is to introduce you to mapping using rasters. By the end of this tutorial, you will be able to:

* Find and use georeferenced historical maps for use as basemaps.
* Calculate the difference in population density between two raster layers. 
* Create a measure linguistic diversity through population density.


## Background
Raster data is primarily used in 3 ways:
* Basemaps (i.e., a georeferenced historical map with contemporary infomation overlaid)
* Surface maps (i.e., population density, rainfall, or temperature)
* Thematic maps (i.e., land use maps)

Raster data is essentially a matrix of pixels (cells) each with a given value. So far, we have focused exclusively on vector data. Vectors consist of points, lines, polygons. Vector data is useful when you have information about an area and want to ask questions about it in relationship to other information about an area. The geometries don't have to be the same (i.e., asking questions that reference data about both points and polygons as in the [QGIS 1](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_3_QGIS1.md) Tutorial). 

Rasters, on the other hand, represent spatial information through pixels. Imagine that the entire surface of the Earth is covered in a grid. Raster data gives each cell in that grid a value (cells "without" a value get 0). So, rather than drawing the boundaries (i.e., census tracts, counties, etc.), we think of the entire area as one unit, divided by pixels. The first layer of pixels determines some attribute about the space. The second layer, another attribute, etc. Calculations can be performed between the layers. The difference between regular images and raster files is that raster files have geographic information associated with them. So though they are both created through a matrix of pixels with different values, rasters are aligned to spatial information (and correspondingly, have a CRS or projection associated with them). 

In this tutorial, we will go over two ways to use rasters. In the first, we will use georeferenced historical maps as basemaps, essentially combining raster and vector data. In the second, we will use two raster layers to analyze population change. By the end of this tutorial, you will be able to:

1. Determine if your project will require rasters or vectors or both
2. Combine raster and vector data in the same project
2. Create a raster file from a vector file
3. Find and import georeferenced basemaps to QGIS
4. Layer your raster data on a historical map
4. Calculate population change through raster layers.



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
 * Keep default Raster size in pixels (3000 x 3000)
 * Load into canvas when finished YES
 * OK
 * Close
3. Nothing changed, now what?
4. Save your project.
5. If your Arabic15Raster.tiff file exists (where you saved it), you have made a raster file!

## Calculate Population Change





 






