# Analyzing Data with QGIS - QGIS Part 2

By the end of this tutorial you will be able to:

* Upload a dataset to QGIS 
* Join datasets based on a shared identifier
* Join datasets based on a shared location
* Query a dataset based on a feature
* Create a choropleth map

## Premise 

We will work with the basemap we made in Tutorial 3 (QGIS Part 1) and add new data to it in order to examine various demographic features of the cities and states where refugees are resettled. If you have not already completed the [Mapping data 00](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/01_MappingData00.md) tutorial please do so before beginning this exercise. 


We will answer a few questions in this tutorial: 

* How many states have populations of greater than two million people? 
* How many states received more than 300 refugees in 2014? 
* How many states with fewer than ten million people received greater than 300 refugees in 2014?

## Set Up

Open your Refugee_Cities.qgs map project.

We already mapped the locations of refugee resettlement in the United States as well as state polygons. We have tabular data available for population at the state level from the [United States Census](https://www.census.gov/) in the Data/state_pop.csv file. The city data also has the number of Refugees per city. We will use these two datasets to answer questions about population and refugee resettlement. In the next tutorial, we will use more detailed information about the cities, including income and infrastructure.


In order to answer these questions we’ll first select just those cities which have populations of more than two million. Then we will export that as a separate layer. 

### Setting up QGIS
<br>
1. Open your MappingData_Population.qgs file. 
<br>
	1. It should still contain the states polygons and cities points we added previously.
	2. If these layers are not immediately visible then **right click** on the name of either layer in the Layer menu and click Zoom To Layer.

### Import population information

Now we will add the table containing population by state which we will join to the state polygons. *QGIS can read several types of tabular data formats, including .csv and .xls files. Our total population file is saved an .csv file (note QGIS cannot read .xlsx files).*
<br>
1. Upload Tabular Data
	1. Click on the Add Vector Layer button 
	2. Add the state_pop.csv file. (Note: we realize it is a little bit confusing that we use the `Add vector layer` button in order to add tabular data to our map project however this is somewhat a product of the fact that QGIS is open source later we will go over how to .csv files which will, more intuitively, be added using the `Add delimited data` button).
<br>
![CSV](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/02_Adding_Layers_Vector.png)
<br>
	3. State_pop should appear in the Layers menu. *Because it is just a table and does not have any geometry, it will not show up in the map view.*
	4. Open its attribute table to see the fields that it contains before we join it to our state polygons. 
	5. Make a note of the columns (or fields) it contains 
	6. This dataset has been pre-cleaned, and the column names have been reformatted. See the tutorial on DATACLEANING for more details.
<br>	
2. Perform a Table Join
<br>
*A table join allows GIS users to combine tabular data with vector data based on an identical field in their attribute tables.*
	1. **Right-click** cb_2014_us_state in the layer menu and select `Open Attribute Table`. This describes the data associated with each feature in the feature class.
	<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/attribtable.png)
<br>
	2. To join attributes from a table to a shapefile the two data sets must share a common attribute field. 
	3. Review the fields in the attribute table for the cb_2014_us_state layer, they are: 
	<br>
* STATEFP
* STATENS
* AFFGEOID
* GEOID
* STUSPS
* NAME
* LSAD
* ALAND
* AWATER

**Note that NAME is identical to stateName, and each is unique -- no two states have the same name. This unique field common to both datasets is what allows us to join the tabular population data to the vector file describing the geometry of those countries. 

We always start the join on the file that we are joining to. We are joining the population estimates table to the state boundary shapefile. 
<br>
1. Open the Properties for the cb_2014_us_state layer.
2. navigate to “Joins” in the left hand menu. 
3. Click the “+” icon. 
4. Make the following selections in the dialogue box.
<br>
![Attribute](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/vectorjoin.png)
<br>
	1. join layer = state_pop
	2. join field = stateName
	3. target field = NAME which matches the join field in the cb_2014_us_state layer.
	4. **Click** `OK` to close the join dialogue. 
	5. **Click** `OK` to close the layer properties menu. 
	<br>
5. Open the attribute table for the countries shapefile. A new field has been joined to the right hand side of the table: state_pop_population
<br>
IMPORTANT!! This joined data is not permanently associated with its attribute table. The relationship only exists within this QGIS project. If we added the cb_2014_us_state layer to another QGIS project the fields we joined from the population estimates would not be there. To permanently incorporate the join, we must save a new version of the shapefile.
<br>
6. **Right-click** on the cb_2014_us_state layer and select Save.
7. Select `ESRI Shapefile` as the format, and save your file in the same folder as the project folder as stateboundaries_pop.shp. 


This new layer will then be added to the map and will contain the  joined data.

## Attribute Tables and Data Querying

Now that we have assembled these data layers we can begin to ask a few simple questions about the data. We will accomplish this by querying the attribute fields of our two vector layers, the populated places and the countries. To do this we will select features using  Select by Attributes. 

There are multiple routes to select features within a dataset. We will follow one, but you may see other ways. We want to select just those states with an estimated population of greater than two million.
<br>
1. Open the stateboundaries_pop attribute table and select select features using an expression
<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectfeature.png)
<br>
2. Make sure the header is correct - we want to select features from the stateboundaries_pop layer
<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectfeaturesscreen.png)
<br>
*If you click on any of the terms in the central box a description of it will appear on the right. We will combine the field name with other operators to build an expression on the left side.*
<br>
![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/15_SelectExpressionMenu_opt.png)
<br>
3. Expand 'Fields and Values and select state_pop
<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selectstatepop.png)
<br>
4. **Double-click**  on `state_pop` and it will appear in the expression box on the right. 5. Open Operators and double-click on the greater than symbol (>). Type in 2000000. Your expression should now look like the following:
<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/greaterthan.png)
<br>
5. **Click** `Select`. Some of the populated_places points should turn yellow. At the bottom left corner of your QGIS project the footer will show how many features were selected (36).
<br>
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/selected.png)
<br>
We will now save those 36 states as a separate shapefile, just like we did for the cb_2014_us_state layer after we joined the population estimates to it. 
<br>
6. **Right-Click** in on the stateboundaries_pop layer, **select** Save As. 
7. Select Save only selected features, and save the shapefile as selectedlayers.shp. This will then be added to our map as a new layer. 
8. To see the new layer, clear your selection by clicking the Deselect features from all layers button.
<br>
![Attribute](https://github.com/CenterForSpatialResearch/MappingForTheUrbanHumanities/blob/master/Tutorials/Images/MappingData01/18_Deselect.png)


##Refugees per state

Now we need to create a layer that will tell us how many refugees went to each state. our city_latlong file has the number of individuals in it. To count the number of individuals per state, we will join the city_latlong to stateboundaries_pop based on their shared location, and then sum the 'Individuals' column.
<br>
1. Select the stateboundaries_pop layer
2. Select Vector > Data Management Tools > Join Attributes by Location
<br>
![Attributes](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/joinbylocation.png)
<br>
3. In the Dialogue box, select the following options
<br>
![Attributes](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/joinlocation_attributes.png)
4. Save as citystaterefugees.shp and click 'OK'
5. Open the attribute table for the citystaterefugees layer. You should see a SUMIndividuals column. This represents the sum of individuals across all the cities in that state. (Don't worry about the NULL values - it just means there aren't any cities in that state where refugees are settled). 
6. Order by number of refugees per state by clicking on the SUMIndividual column header.
7. What state received the most refugees? 
8. Click on that row (by clicking on the number on the far left). Move the attribute table out of the way so you can see the map again. That state should be highlighted. You can select multiple rows by holding the "Command" button and clicking on the rows you are interested in.
9. Close the attribute table and Deselect Features from All layers

![features](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/deselect.png)
10. Select the `select features using an expression` tool. We will again select by expression in order to select the states with greater than 300 refugees. Use the expression builder as we did above to select the states. Your expression should read:  `"SUMIndividuals"  > 300`

The footer bar of the map will indicate that 14 features were selected. 

Use this selection to identify which states of greater than 300 refugees are within countries with fewer than ten million people. Use the expression builder to figure out which 6 states have these two characteristics. *Hint: You will need to use 'AND'*
11. SAVE your project

##Creating a map

Now that we have calculated information about the number refugees in each state, we can represent that in different ways in the map. We will make a chloropleth map to represent refugees by state. We will then go over cartographic conventions adding a legend and scale bar to the map and exporting as a PDF. 


We will create a choropleth map for refugee population by state, where each state will be colored according to the number of refugees who settled there in 2014. 
1. **Open** the properties for the citystaterefugees layer and navigate to the Style tab.
2. Select Graduated Symbols from the dropdown at the top

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/graduated.png)
3. Select SUMIndividuals as the Column on which we will color the map. 
4. To change the color of the entire state polygon, we need to change the symbol from an outline to a filled polygon.
5. Click the Change button next to Symbol and select “simple fill.” 
6. Next  break up the data into classes (ranges of values) and classify the colors for the choropleth map according to these. 
	1. Change the mode to Natural Breaks (jenks), and the number of classes to 8.
	2. **Click** `Classify`. Your properties menu will now look like the one below. 

![Attribute](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/jenks.png)
	3. Click `Apply`. The country polygons will change on the map. 
7. Some states stayed the same color as the base color. These states do not have any relevant data. That is, no refugees were resettled there in 2014.



####Designing a map
In order to present this map, we will now compose a map layout and become familiar with the QGIS map composer. The map composer allows you to add a legend, north arrow and scale bar to the map as well as to export our work as a PDF. 
1. Open a new map composer 

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/composer.png)
2. To add a new map to the composer select the add new map button. 
3. Then click once and drag a rectangle over the area on the page that you would like the map to occupy. *Whatever is showing in your QGIS map project window is what will appear in the new map.*

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/composenewmap.png)
4. Add a legend. 
	1. Select Add new legend. 
	
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/addlegend.png)
	2. Again click to draw a rectangle where you would like to place the legend. An unformatted legend that matches the information from the Layers panel will appear. 
	3. Use the options in the Item Properties tab to change which layers are represented in the legend and to change the labeling of the layers in the legend.
	4. Select the 'Item Properties Tab
	5. Unselect 'Auto Update'
	
![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/itemproperties.png)
	6. Remove Unnecessary layers with the '-' button
	7. Change the layer names by clicking the “legend item properties” button

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/customlegend.png)
5. Add a scale bar. 
	1. Select Add new scale bar button. 
	2. Again you will be able to change the properties of the scale bar, including the style, number of segments and size. 

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/scalebar.png)
6. Add text boxes
	1. Add a title for the map 
	2. Add abbreviated citations for our data sources. 
	3. Click the add new label button then use the Main properties field to add the text, and use the Font button to change the text size and font. 

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/textlabel.png)

Finally use one of the export options circled in blue above to save the map composition as an image file, PDF, or SVG. 

![feature](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/saveas.png)

______________________________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered by the [Center for Spatial Research](http://c4sr.columbia.edu) at Columbia University in Spring 2017. 
It is based on the tutorial written by Dare Brawley, for *Mapping for the Urban Humanities* taught in Summer 2016 also by the [Center for Spatial Research](http://c4sr.columbia.edu).


