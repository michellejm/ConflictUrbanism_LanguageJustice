# Tutorial 7: Data Visualization

March 7, 2017

This tutorial covers the very basics of data visualization and digital storytelling, covering visualization types, features to consider and important design considerations. The purpose of this tutorial is to help you create informative, appealing visuals to accompany your final project. 

By the end of this tutorial, you will be able to:

1. Determine which type of visualization will best represent your data
2. Identify features of a "good" visualization
3. Decide when to use raw data and when to transform it


## Part I - Data and Statistics

The most important part of any visualization is the data. Data can refer to "big data" (extremely large datasets), just a few hand curated data points, or anything in between (i.e., census data). Sometimes the raw data is not best to illustrate the story you want to tell. In those cases you want to transform it. 

Basic Data transformations

1. Mean, Median, Mode
  1. Mean - this is the average you are used to (add all the numbers and divide by the total)
  2. Median - the number in the middle, this helps account for outliers
  3. Mode - the number that occurs the most often
  
An EXCELLENT resource for thinking about statistics is [here](http://students.brown.edu/seeing-theory/). This was made with D3, a javascript library for making interactive, reactive visualizations.
  
2. Real, Ranked, Percentage (2011-2015 American Community Survey)
  1. Real numbers are the raw data so there were X Vietnamese speakers reported in the census in 2011-2015 for each county
  Bronx: 2871
  Brooklyn: 3272
  Manhattan: 1365
  Queens: 2712
  Staten Island: 507
  Total: 10729
  
  2. Ranked: 
  27th most common language out of 40 languages
  This is in the 33rd percentile. So, among languages spoken at home, 67% of languages are more common than Vietnamese.
  
  3. Percentages
    1. Percent of Vietnamese speakers in each borough:
      * Bronx: 30%
      * Brooklyn: 29%
      * Manhattan: 13%
      * Queens: 25%
      * Staten Island: 4%
      ![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/vietnamese.png)
    2. Percentage of each borough that speaks Vietnamese:
      * Bronx: 0.22%
      * Brooklyn: 0.14%
      * Manhattan: 0.09%
      * Queens: 0.13%
      * Staten Island: 0.11%
      * New York City: 0.14%
    
 That's fine, but often change tells a more compelling story. 

1. Let's look at 2006-2010 ACS data as well. Taking the middle year, here, we will treat this as 2008, and the 2011-2015 as 2013.
2. From 2008-2013, there are 2 more Vietnamese speakers living in NYC, though 300 of them moved from the Bronx to Manhattan and Brooklyn. 
3. Let's look at a group of speakers who have seen more change in that time: 

  1. Speakers of African Languages: 35% growth
  
  2. Speakers of Arabic and Armenia both saw 32% growth. That's a change of 1062 people for Armenian and 13,871 for Arabic. This might suggest a potential increase in the Armenian community in the coming years. 
  
  3. At the same time, 54,064 Chinese speakers arrived, but that was only a 13% growth from 2008. The greatest number of arrivals was from English Monolinguals, with almost 100,000 individuals, though only a 3% increase in people.
  * Chinese       54064	13%
  * Spanish       70436	4%
  * EnglishMono   99172	3%

4. What about who left? Well, it seems to be a mixture
  * Italian   -18986	-19%
  * Mon-Khmer -302		-12%
  * Gujarati  -1085	  -11%
  * Greek     -4936	  -10%

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/lngchng.png)
There's a story behind each of these statistics that can be told with a mixture of images, graphs, maps, and audio.

Italian and Greek speakers represent very old immigration, so now that many are 3rd generation, they may not speak the language. Of the older people, many may be moving or dying and not necessarily being replaced by newcomers. 

What about Mon-Khmer and Gujarati speakers? First, Mon-Khmer is a language family (of which, Vietnamese is one language), not just one language. This probably refers to MK speakers from Cambodia, a group that has been [slowly shrinking](http://www.nytimes.com/2008/01/20/nyregion/thecity/20camb.html) in New York City for some time. Gujarati is spoken in India, mostly on the border with Pakistan. There is a Gujarati newspaper based in the city, and a long history of Gujaratis in NYC. So, what's happening? Gujaratis also have a very long history of immigration to the US, as many started arriving immediately after the 1965 Immigration and Nationality Act. So this decrease may also be to a slowing of immigration, movement to NJ and death without replacement. 

What about the bigger languages?
![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/top3chng.png)

In this way, the data helps to get the story started. 

## Part II - Questions

1. Question formation is usually a combination of interest, curiosity, and what data is available. 
We have two data sets: 
  * 2006-2010 American Community Survey (language spoken at home)
  * 2011-2015 American Community Survey (language spoken at home)
We also have a precalcuated table of changes between these two datasets

Download all of the datasets [here](https://drive.google.com/drive/folders/0B8IdSWLrkSd3bWx6NnByWGNZUTQ?usp=sharing)

2. Start with a cloze exercise:
  1. There has been the greatest increase in ____________ speakers since 2010.
  2. ____________ has the most English monolinguals.
3. Write 2 more cloze statements.

## Part III - Exploratory Visualization

1. Open these datasets in Excel.
2. Answer your two cloze statements. 
3. Create one plot just using Excel's defaults where a user could find the answer. 
  1. If you have never used Excel's graph making tools, we will make these together.
  2. If you have used Excel's graph making tools, make 1-2 graphs to illustrate your cloze statements. 

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/top5growth.png)


Using the Excel Defaults

1. We are going to make the first map: Growth in Speakers of a Language other than English in New York City 2008-2013 (top 5 languages)
2. In the LanguageRows Tab, each row represents a language and each column represents a borough/year combination and calculations about the differences between each. This format (each language in one row) allows for easy comparison between the languages (rather than comparison between the geometries). 
3. Sort the sheet by 'PeopleChange' (Column P - lowest to highest - your sheet has 'headers')
4. The top 5 languages are at the bottom.
5. Copy these 5 languages (exclude 'English' and 'Total') and paste them on a **new tab** (this isn't exactly necessary, but will make it visually easier).
6. Copy the corresponding values and Paste-Special as 'Values' on the new tab
7. Also Copy and Paste-Special the **PplChng Columns** (Columns V-Z) on the new tab. We may not get back to it, but there are some interesting things in here (look at Chinese in the Bronx)
8. On the new tab
  1. Select the A1:B6 cells
  2. Under 'Insert', Select 'Column', 'Clustered Column'
  3. Your graph should appear.
  3. Change the title by double clicking on it.

Let's answer the other cloze. 

____________ has the most English monolinguals.

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/EngMono.png)

1. In the **Language Columns** Tab, each row represents a borough, and each column represents a language. This format allows for easy comparisons between the boroughs. 
3. Copy the cells corresponding to  English-only percent_speakers/Bronx-Staten Island_2011-15 (D20:D24) 
4. Paste-Special on a new tab in column B
5. Go back and copy the borough names & past on the new tab in column A
8. On the new tab
  1. Select the A1:B5 cells
  2. Under 'Insert', Select 'Column', 'Clustered Column'
  3. Your graph should appear.
  3. Change the title by double clicking on it.
  4. Remove 2011-15 either through Find & Replace or manually.

This gives you a way to better understand your data.

### Exploring the Explanations

What makes a good Exploratory versus Explanatory visualization?

What are the goals of the visualization? What story are the authors trying to tell? Why? How? **Is** there a story being told or is the viewer invited to follow their own narrative?

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/nobel_large.jpeg)

1. A viewer of the Visual History of the Nobel Prize and Nobel Laureates could take one of many paths through the visualization and come away with many different interpretations. 
2. While some types of data were highlighted, others were not (i.e., what industry they work in (in/out of academia), if they have children, etc.)
3. Some data points were highlighted (lower right corner), offering explanatory examples.

On the other hand, 538 did a great piece explaining [why Katie Ledecky is so phenomenal](https://fivethirtyeight.com/features/katie-ledecky-is-the-present-and-the-future-of-swimming/). They are telling a story, and telling it very linearly, but the data drives the way the story is told.

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/ledecky.png)

On the other hand are more qualitative stories that incorporate data only to underscore the point. There's NYT story covering [the war in Yemen](https://www.nytimes.com/interactive/2016/12/16/world/middleeast/yemen-war-saudi-arabia-we-visited-the-place-the-world-has-forgotten.html) and another about [Simone Biles](https://www.nytimes.com/interactive/2016/08/05/sports/olympics-gymnast-simone-biles.html?module=Article&region=TopBar&action=Click&pgtype=Multimedia). Both of these use visuals to tell a qualitative story rather than a quantitative one, incorporating data to illustrate the point.

#### Considerations with a visualization

1. Infographics versus Data Visualizations
  1. Infographics *tend* to be story-heavy rather than data-heavy
    1. May include visual scaffolding or context.
    2. Include data and statistics to tell a story 
    3. Heavy on story, light on charts and graphs. 
    5. Often "hand-drawn" with Adobe Illustrator or similar software. Author makes individual choices about position, size, color, styling for each element
    
  2. Data visualizations *tend* to be data-heavy rather than story-heavy 
    1. Usually made programatically with D3 or Python+MatPlotLib or even Excel
    2. Because the visual draws automatically from the data, can be used with an API to get "real-time" data
    2. The focus is on clear presentation of the data, not on telling a story
    3. Emphasis is on clarity and minimalism rather than delivering contextual information
    3. Generally used to support other findings or with some written context
    
2. Data Types
  1. Categorical
    1. Nominal (countries, gender texts) 
    2. Ordinal (rankings, likert scales)
  2. Continuous
    1. Interval (temperature, dates/times) - the distance of measurement is the same, zero is arbitrary, and fractions don't make sense (i.e., 60 deg is NOT twice as hot as 30)
    2. Ratio (people counts, money) - there is a 0 count (i.e., there are 0 Navajo speakers, there are 300 Vietnamese speakers, and more than twice as many Japanese speakers).
    
2. Dimensionality of the data
  1. How many variables does your data have?
  * For example, 'Language spoken at home' and 'Neighborhood' is easy to visulize many ways (maps, charts, etc.).
  * 'Language spoken at home', 'Neighbhorhood', and 'Dual language schools' would be a little harder, but 
  * 'Language spoken at home', 'Neighbhorhood', 'Dual language schools', 'ELA scores', and 'Income' would be much harder.
    1. Are any variables dependent upon another?
    2. Are any variables redundant?
  2. Do all of the variables need to be represented on the same chart?
    1. Could they be separated?
    2. Would it make sense to break them up across multiple charts represented the same way?
    ![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/5boros.png)
    
2. Visual Contrast - viewers expect each of these things to mean something. This cart is from [here](http://paldhous.github.io/ucb/2016/dataviz/week2.html). The reference is [here](https://ils.unc.edu/courses/2015_spring/inls541_001/Readings/Cleveland%20and%20McGill%201985%20-%20Graphical%20Perception%20and%20Cleveland1985-Graphical%20Methods%20for%20Analyzing%20Scientific%20Data.pdf)

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/class2.jpeg)

  1. Position along the axis
    1. Good for continuous variables (i.e., time, distance, etc.)
    2. Poor for categorical 
  2. Size
    1. Good for continuous variables
    2. Poor for categorical
  3. Color ([color brewer](http://colorbrewer2.org/) and [coblis](http://www.color-blindness.com/coblis-color-blindness-simulator/)
    1. Good for categorical variables
    2. Bad for continuous (except chloropleth maps)
  4. Shape
    1. Good for categorical variables
    2. Impossible for continuous


3. Visual math is hard to do
  1. [This chart](http://lotrproject.com/blog/2013/01/15/character-dialog-in-the-hobbit-an-unexpected-journey-measured/) asks you to subtract the red from the grey to calculate differences in the grey. 
  ![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/hobbit.jpeg)
  2. A clearer approach would be to make another chart, pulling out what they want you to understand from the visualization.
  
3. Scales
  1. Scales should ALWAYS start at 0. Not doing so deceives the viewer [example](http://flowingdata.com/2012/08/06/fox-news-continues-charting-excellence/)
  3. If there are extreme outliers remove them and indicate them elsewhere.
  4. You can always split the data if they are on different scales (see the examples above)
  5. The scale should size to the data to show variation in the most representative way
  
4. Labels
  1. Do use labels for all variables
  2. Don't label redundantly (i.e., a label on the chart AND next to it)
  3. Do minimize visual clutter by using larger intervals (i.e., label every 5 years rather than every year, etc.)

## Chart types

#### Basic Charts (1-3 variables)
1. Bar charts 
  1. Humans are so good at this (see above). Often start with a bar chart to get a sense of the data and then decide a better way to represent it.
  ![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/top5percent.png)
	2. Grouped bar chart (2 datapoints)
  	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/yiddish_hebrew.png)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/lolConc.png)
	3. Comparison within groups (stacked bar chart) [citation](http://peltiertech.com/diverging-stacked-bar-charts/)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/stacked.png)
	4. Relative value, strength of category (stacked percentage bar chart)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/digital2.png)
2. Bar chart vs. Line chart?
	1. Bar charts are categorical (i.e, this much or this many in this bin)
	2. Line charts are continuous (i.e., this much or this many at each point along this interval)

3. Line charts
	1. X axis must have a CONTINUOUS variable (i.e., time, distance, temparature)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/DRMobile.png)

4. Pie Charts
	1. Though they are common, often used poorly. 
	2. Best for showing 2-3 categories
	3. Terrible for showing slight variations (or good for hiding slight variations)
	4. Compared to bar charts, arcs are challenging to visually understand
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/txtlng.png)
5. Scatter plots
	1. Good for showing correlation or patterns
	2. Only 2 variables
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/acad.png)
6. Bubble charts
	1. Good for showing 3 variables - like a scatter plot with size added
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/Sonority.png)
7. Area chart
	1. Like a line chart, but with the area under the line filled in. A good example is [here](https://research.google.com/bigpicture/music/)
	2. Best to represent volume of a variable over time (i.e., records, or, with enough data, people)

#### More Variables

1. Box plots (usually for financial data)
	1. Good for multiple variables, outliers, and ranges [example citation](http://www.datamology.com/sample-BA.shtml)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/sample.jpeg)

2. Heat maps
	1. Good for groups compared to other groups (time of day, day of week, web visits) [example citation](http://help.plot.ly/plotly1/make-a-heatmap/)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/okc.png)
	
3. Radar or spider charts
	1. multiple variables at a time. These are extremely difficult to parse. Do not use them if you want your readers to understand what you're saying. [example citation](http://www.datavizcatalogue.com/methods/radar_chart.html)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/radar_chart.png)

4. Parallel coordinates
	1. Each line going across shows the data point, can see relationships between variables (I've seen few good examples outside of biology) [example citation](https://www.computer.org/csdl/mags/cs/2015/03/mcs2015030070.html)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/sepal.png)

5. Tree Map
	1. Size based relationships [example citation](http://flowingdata.com/2015/02/06/baking-units-demystified/)
	![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/units.png)
	
#### For Fun
1. The NY Magazine [Approval Matrix](http://nymag.com/arts/all/approvalmatrix/approval-matrix-2016-09-05/#)
2. 
	
On deciding [which chart type to use](http://extremepresentation.com/wp-content/uploads/6a00d8341bfd2e53ef0148c699cc96970c.jpg)
![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/charttype.jpeg)

## Making a Visual

1. Excel
2. Google Sheets
3. [Plot.ly](https://plot.ly/) for embedable, interactive charts (freemium)
4. D3

#### D3

D3 is a Javascript Library that is often used to make interactive charts and graphs. Libraries are like sets of commands we give to a programming language. Javascript is the 3rd web-based programming language. It makes the interactive things on websites. Javascript alone does a lot, but D3 specializes in making beauitful data-driven graphics. There are MANY examples on the [D3 website](https://d3js.org/) and around the internet ([Mike Bostock](https://bl.ocks.org/mbostock), [D3 Wiki](https://github.com/d3/d3/wiki/Gallery), etc.). In this tutorial, I am going to provide you with an HTML template that you can embed into your HTML page. Because it is interactive, we will need to get a local server running on our computers. 

If you didn't download your datasets before, download them [here](https://drive.google.com/drive/folders/0B8IdSWLrkSd3bWx6NnByWGNZUTQ?usp=sharing)

**Get a local server up and running**

### (Mac) Check which Python version you have (if any)

1. Open a Terminal Window 
![terminal](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/terminal.png)
2. Type `$ python -V` hit 'Return'
3. Something like this should appear. 
![python](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/pythonv.png)
4. Make a note of which Python version you have, you will need it later.

### (Windows) Check which Python version you have (if any)
1. open Command Prompt
2. type python --version hit 'Return'
	* if python is installed something like this will appear
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/pythontest.png)
	* if it isn't then a message stating that will appear
	* if Python is installed make note of which version you have installed, you will need it later
3. if python is not installed then go to [python.org](python.org) to download python. We recommend installing version 2.7. 
4. After downloading the installer, double-click to open it and follow the installation prompts, selecting the defaul settings until you get to the page that reads "Customize Python 2.7.XX" 
	* Scroll to the bottom of options, and click the drop-down selection that reads "Add python.exe to Path" (it should have a red "X" by default)
	* Select the option that reads "Entire feature will be installed on local hard drive"
5. Follow the prompts on the rest of the setup, allow the installation to finish. When it's done, it will tell you, and python is now installed on your computer and available to use.
6. To test that python was installed, open the Command Prompt application, and enter python --version. It should read "Python 2.12.XX". 

### (Mac) Set up a local server

We will run a local server from our computers. The details of this are far beyond this tutorial, for more on  the technical details, visit the [Mozilla Developer site](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Set_up_a_basic_working_environment). For more on how the web works the difference between a local and remote server, [read this](https://devdojo.com/blog/technology/local-vs-remote-servers).

1. In a Terminal window, navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Desktop > CULJ > d3. To navigate there, I type the following commands (don't type the $, that just indicates that you are in the Terminal):

	* `$ cd Desktop`
	* `$ cd CULJ` 
	* `$ cd d3`
	
2. If you have Python 3, type:

	* `$ sudo python -m http.server 1010`  (you can pick your favorite 3 or 4 digit number)
	
2. If you have Python 2, type:

	* `$ sudo python -m SimpleHTTPServer`
	
	It will look something like this:
	![server](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/server.png)

3. Return to your browser window (Chrome, Firefox, or Safari) and type `localhost:1010` in the navigation bar. You should see an empty webpage. 

We will come back to this.

###(Windows) Set up a local server
1. Open Command Prompt. Then navigate to the folder where you have saved your html file (directions below on how to "navigate"). In my case it is in Desktop > CULJ > d3. To navigate there, I type the following commands:

	* cd Desktop
	* cd lCULJ
	* cd d3

2. If you have python 2 type:

	* python -m SimpleHTTPServer

3. If you have python 3 type: 

	* python -m http.server

	It will look something like this:
	![img](https://github.com/CenterForSpatialResearch/NYCDHWeek/blob/master/Images/localhost.png)
3. Return to your browser window (Chrome, Firefox, or Safari) and type `http:\\localhost` in the navigation bar. You should see an empty webpage.

We will come back to this.


#### The template

Open the barchart.html document with Sublime or Text Wrangler

1. Notice this is structured just like the HTML document for your Case Study Template EXCEPT that the css is in the header because there is very little CSS associated with this chart and it is very specific to this graph (i.e., you wouldn't necessarily want a universal color combination, though you may want MORE universals than we have established).

2. The next block tells this HTML page to read from the d3 website to understand the instructions we are about to pass to it. 

3. Javascript uses a lot of 'var' to set the variables. Every time you see 'var', it is passing JS a container full of instructions. At the end, these instructions are compiled. 

4. d3.COMMAND specifies that that command is part of the d3 library

5. There are few things we have to change.
	1. Find where the data is coming from. HINT: we are telling d3 to looks for a tsv file, who's extension is actually a txt.
	2. When we said that data visualizations are made programmatically, this is largely what we meant - that the file that contains the data is separate from the commands that turn the data into a visual. 
	3. d3 reads this as if it were a database. It first looks for a header for each column. 
	4. When we *call* the file, we assign it a function, d. *function* is a special word *d* is something we chose randomly. Once we pass it the function and assign it the name, d, we tell it where to find the values. We say look in the VALUES column.
		1. Replace the word 'VALUES' with the name of the corresponding column in our txt file. 
	6. Now we have to tell it where to find the X values. 
		1. In the next block of text, we define the x domain and assign a new function, d, and tell it where to find the names of our categories. 
		2. Replace the word 'CATEGORY' with the name of the corresponding column in our text file.
6. Each instance of 'append' places something on the graph. 

Now, return to your browser and refresh the page. You should either see your visual or a list of files, click on the appropriate file. 

If your graph is not appearing, we need to debug and check that the code is right and the data and HTML files are both in the same folder. 






__________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered by the [Center for Spatial Research](http://c4sr.columbia.edu) at Columbia University in Spring 2017. 
   
