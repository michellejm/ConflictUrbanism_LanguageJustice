# Tutorial 6: Data Cleaning

By the end of this tutorial you will be able to:

* Download an original dataset from NYC Open Data
* Modify that dataset to suit your needs
* Clean the dataset so it can be used in various formats
* Strategically use exploratory visualizations to better understand the dataset

For this tutorial, we are going to take a publicly available dataset from the Internet and map some of the datapoints. Most datasets will need some cleaning before they are ready to be worked with; there are usually some errors, missing information, duplicate information, etc. Therefore, we need to clean this dataset before we begin using it. 

*Our questions:*
Community Centers in New York City offer a variety of services from classes to family support to immigration help and much more. This is an exploratory mapping exercise where we want to know how these services are situated in the city.

1. Go to [NYC OpenData](https://nycopendata.socrata.com/). As you can see, there are a lot of datasets available categorized under a variety of topics.
2. Use the search bar to find datasets that reference **immigration**. You will be presented a list of Datasets.
3. Select DYCD after-school programs: Immigrant Services
4. Select 'View Data'
![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/clview.png)

4. Spend a few minutes getting acquainted with the data.
	1. What do all of the columns mean?
	2. Are there any columns that are going to be irrelevant to your project?
	3. Is there spatial information in this dataset? What does it look like?
	4. What problems do you see with using it?

5. Export the data and download it as a csv file. ('Export' is light blue on the far right side)

6. Go to Excel and open a new spreadsheet. You *may* be guided through a series of steps asking how the data is delimited. It is 'delimited', not 'fixed-width'. "CSV" stands for "comma separated values", so select 'comma', and keep the quotes for delimiting text. 

7. Click 'Next' and 'Finish'. **STOP** *Does the data look how you expected it to look? Why or why not? What happened? How can we fix it?

8. On using Excel

	1. There are many tools to clean data, and if you are going to work with very large datasets regularly, you will want to learn Python+Pandas, R, SAS, or another programming language. However, for our purposes, you do not need anything more powerful than Excel.
	2. The data we are going to work with is relatively "clean." Most datasets made available by governments and large institutions are "clean", meaning that there are very few errors, duplicate entries, misspellings, alternative descriptions, etc. 
	3. The messier the data, the more powerful tool you will need. For working with very messy data without learning a programming language, I suggest [Open Refine](http://openrefine.org/)

**Plan for cleaning**

1. Remove duplicates

2. Handle missing values

3. Conversion issues (i.e., numbers rendered as dates, etc.) 

4. Separate cells with multiple pieces of data, concatenate cells if needed

5. Trim leading and trailing white space

*Data from different sources will need different approaches, this is appropriate for this particular dataset.*

**Steps**

1. Prepare the workspace. When cleaning datasets, it is far too easy to make mistakes, forget where you are, and otherwise get confused. This step helps prevent that.
	1. Make four tabs (sheets) in your Excel Workbook - 'Original', 'Working', 'Final', 'Incomplete'
	![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/fourtabs.png)
	2. Don't change the Original tab
		1. Make a copy of the data and paste it into 'Working'
		2. Select all of the cells by clicking on the cell in the bottom right and pressing 'Command' + a
	3. Remove Duplicates (this step comes early because in the next step, we give every row a unique ID)
		1. Select the entire sheet by clicking in the upper right hand corner.
		2. Select Data > Remove Duplicates
		3. You will be prompted with a dialoge box, Accept the duplicates if you think it is correct.
		![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/duplicates.png)
	4. Move the first column, 'Program Type', to the end. Since the data in this column is descriptive rather than identifying, I prefer to have it at the end.
	5. Add a column to the left of 'Program', this will be in column A, label it 'ID'
	
		1. Insert a row and typing 1,2,3 and carrying it to the bottom **OR**
		
		2. Highlight all of the cells by clicking on the first and then Shift+click on the last cell and then select Edit > Fill > Series 
		
	5. At this point, I like to rename the columns into single words (i.e., 'Age Group' > 'AgeGroup'), make the column names bold, and freeze the first row and first column.
	![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/Freeze.png)

2. Missing Data

	1. Each Row that is missing an address needs to be removed from the data set since we cannot map it. 
		1. Cut and paste these rows into the 'Incomplete' Tab. We won't be able to map this datapoint without finding more information.
		2. Since we are only concerned about the addresses, one way to do this is to sort the sheet by addresses and remove the blanks.
		
	2. Each Row that has a missing Age Group should stay in the dataset but **also** be added to the Incomplete tab, in the hopes that we might do other searches to fill in the blanks. 
		1. Copy and post these rows into the Incomplete Tab
		2. Fill in the missing values with a null value (i.e., 'Unk', 'NaN', or another value. This is just good practice as some systems will crash without *something* in every field).
		
	3. Select all of the cells again and find any remaining empty cells.
	4. We can return to these datapoints later if we decide to use this dataset for a project.
	
3. Fix errors created by converting to Excel
	1. There are two dates (May 20 and Nov 14) that have been automatically created by Excel
	2. To override Excel's automatic formatting, change the datatype in this Column to 'Text'
		1. Format > Cells > Data Type > Text
	3. Go back to the original data to find the correct values
		1. (May 20 is Age 5-20; Nov 14 is Age 11-14)
	4. Enter the correct ranges.

4. Separate Addresses *Location contains both address information and latitude/longitude - it would be easier for us to have latitude/longitude available*
	1. First take a look at the cells with the location information in them. There are multiple lines per cell. We need the information in one line. We are going to use an Excel formula to collapse those lines, and will be a little clever about it because there is no direct way to do this. 
	2. Insert FOUR columns to the right of 'Location'.
	3. Type this formula into the first cell of the first column (probably Column I: =SUBSTITUTE(H2,CHAR(13),"\")  
		- *This means take cell H2, find Character #13 (the carriage return) and substitute the backslash.* This was a bit of trial and error as it could have also been Character #10 (new line).
		1. If your Location column is in a different place, change H2 to the relevant location.
		2. Drag this formula to the bottom of the data to fill in all of the cells.
	3. Copy this entire column, and Paste Special > Values into the same location. 
		- You have to do this step for Excel to recognize the data in these cells rather than just the formulas.
	4. Select the entire 'Location' column again if it isn't already selected (the new location column you just made).
	5. Go to Data > Text to column
	![image](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/TExt2Columns.png)
		1. Select 'Delimited' 
		2. Select \
		3. Finish
5. Separate Latitude and Longitude
	1. Select the column with latitude and longitude in it
	2. Insert a column to the right
	3. Select text-to-columns
	4. Select 'Delimited', 'comma-separated', Finish
5. Remove the parentheses
	1. Select the Latitude column
		1. Find and Replace the character, ( , with nothing	
	2. Select the Longitude column
		1. Find and replace the character, ) , with nothing
6. Rename the columns appropriately
	1. I chose Location2, Street, City_State_Zip, Latitude, Longitude	
5. Select all of the data in this sheet and copy it onto the Final Tab.
6. Save it
	1. From the Final Tab, select Save As > csv, and rename it something easier to type. (I chose ' *This will only save this sheet. That is OK - that is all that you want.* )
	2. **Also** save the whole workbook 
	
**Congratulations! The data is clean enough to work with!**


## Visualize it

Now we want to get an idea of what this looks like against a map of New York City. I best understand New York using the neighborhoods as a guide rather than the census tracts or just the boroughs. So, I'm going to use the neighborhood tabulation area map as the basemap and visualize this layer on top of it. This tutorial will use QGIS, you can use Carto if you would prefer.

1. Open QGIS

2. Import a Vector layer 
![vector](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/vectorlayer.png)
	1. Select Import Vector Layer
	
	2. Add the nynta.shp file from the [Data Folder](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/tree/master/Data) on Github.
	
	3. Change the Coordinate Reference System to "NAD83 New York State Plane Long Island" The EPSG Code is 2263. If you don't remember how to do this, revisit [Tutorial 3](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Tutorials/Tutorial_3_QGIS_part1.md)
	
*We are using this CRS because it is the one most often used by city agencies when preparing and analyzing their datasets. For such a small area, projection is not going to significantly affect the results. In your final maps, you may wish to use a different projection for aesthetic reasons. However, for analysis, we will use the most accurate and most commonly used projection for New York City.*
	
3. Add the data we just cleaned

	1. Select Layer >> Add layer >> Add Delimited Text Layer
	![delimited](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/Delimited.png)
	
	2. Add the file we just cleaned
	
	3. Select csv (the button will turn blue)
	
	4. If x-coord and y-coord did NOT autofill, select the appropriate columns
		1. X: longitude
		2. Y: latitude
		
	5. Select OK
	
	6. Select the Coordinate Reference System 

4. If the points do NOT appear:

	1. Click on the Zoom Full Magnifying Glass
	
	2. Make sure that the points and the base are not the same color
	
	3. Double click on each layer and make sure you are using the same CRS

5. What do you notice about this map?

	1. Are there clusters of services?
	
	2. Do services exist along any particular shape?
	
	3. Are there any service deserts?
	
	4. Does looking at this map present further questions about distribution of immigration services in NYC?


To complete this tutorial, send your exploratory map as a pdf or jpeg to Michelle at mam2518@columbia.edu

## Next steps

I would like to know which language speakers have access to the most access to immigration services. Are any groups being underserved? What would we have to do to answer this question? How could we bring in data about languages in the city to get a better answer to this question? Do transportation routes matter?


## Advanced

Download the 2011-2015 American Community Survey Dataset

Data cleaning plan:
1. Remove columns we are not going to use. We only want number of speakers - not how well they speak english
2. Create a column that matches the census tracts clipped to shoreline so we can do a column join
3. Get subtotals for each borough
4. Calculate percentages from the raw numbers


1. Create the data management 4 tabs. Add 1 more tab: Extras
Step 1 - Remove columns will not use. It is MUCH easier to remove rows than columns

1. Select all of the cells from the original tab. Do this by clicking in one corner and then 'Shift'+'click' in cell II2168 (the bottom cell of the sheet)
2. Copy these.
4. Go to the 'Working' Tab and 'Paste Special' - Transpose the data.
5. Freeze the top 5 rows.
6. Copy the entire workbook (click in upper left corner) and Paste-Special (Values)
8. Insert 2 columns to the right of the ID Column
9. Use 'Text-to-columns' to separate on the colon
6. highlight row 6 to the end by selecting the entire row 6 and pressing "shift" + "click" on the last row (you have to click on the little numbers)
11. Sort by column C
12. Cut all rows referencing 'Speak English' and paste them in the Extras tab.
13. Insert the headers above this on the Extras Tab
14. Sort to consolidate the 'Margin of Error' and move these to the Extras tab also
15. Delete Column C
16. Remove the ' - ' from the languages.
17. Move all of the languages over under the 'ID' Column
18. Delete Column 'B'

Step 2 - Create a column that matches the census tracts clipped to shoreline so we can do a column join
1. This is in the wrong shape now so we need to transpose it back. You can't do this on the same sheet because of the shapes. So make ANOTHER Tab - Call it 'Working2'
2. Paste Special - Transpose
3. Insert a row next to 'County'
4. In cell F2, write =CONCATENATE(D2, ", ", E2)
5. Drag the bottom corner to fill ther rest of the Column. 
6. Call this Column 'GEOID'
7. Copy & Paste Special as Values

Step 3 - Get subtotals for each borough
1. Under Data is a 'Subtotal' Tool
2. At every change in 'County', SUM all of the languages
3. To just see the counties, select the tiny '2' on the far right side - this will collapse so you only see the subtotals. 
4. To use these separately, create another tab, called 'Borough'
5. Select each of these rows individually by clicking on each row while holding the 'Control' Key
6. Copy & Paste Special - Values in the new sheet.
7. Copy the entire header row and paste it into the new borough sheet also

Step 4 - Calculate percentages from the raw numbers
1. Copy the languages from "Speak only English" to "Other and Unspecified"
2. Freeze panes so you have some orientation.
2. Paste them in the rows next to the raw data. 
3. In cell AV2, type this formula: =H2/$G2
	1. The $ make the G column stay constant. 
	2. If you ALWAYS wanted to divide by cell G2, you'd type $G$2. 
	3. If the total number of speakers was in ROW 2, you'd type G$2
4. Use the bottom left corner to fill across and down for all the tracts and all the languages.
5. While it is highlighted, Right click to Format Cells. Change it to 'Percent' with 0 decimal places.

Done!! Your data is ready to be joined to the 2010 Census tracts file clipped to shoreline or used for data visualization.

__________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered by the [Center for Spatial Research](http://c4sr.columbia.edu) at Columbia University in Spring 2017. 




	

