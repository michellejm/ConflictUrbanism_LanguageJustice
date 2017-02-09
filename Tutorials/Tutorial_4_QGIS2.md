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

First, we are going to take a vector file and turn it into a raster file. 
1. Open QGIS 
2. Add a vector layer
3. Add the `NYCT-Langs_ACS5YR_2015` Shape file
  * This file was created by joining census data to the 2010 census tracts that have been clipped to the shoreline (nyct2010_16d). The data wsa cleaned and modified to allow a column join. The values were then transformed from integers to real decimals with a precision of 2. For more on data cleaning, see [Tutorial 6](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_6_DataCleaning.md)
4. This file will appear as census tracts for New York City. 

5.  





