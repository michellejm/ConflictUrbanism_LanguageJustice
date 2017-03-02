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

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/LangChng.png)
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

Download all of the datasets [here](

2. Start with a cloze exercise:
  1. There has been the greatest increase in ____________ speakers since 2010.
  2. ____________ has the most English monolinguals.
3. Write 2 more cloze statements.

## Part III - Exploratory Visualization

1. Open these datasets in Excel.
2. Answer your two cloze statements. 
3. Create one plot just using Excel's defaults where a user could find the answer. 
  1. If you have never used Excel's graph making tools, we will make one of the following three together.

![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/top5growth.png)
![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/top5percent.png)
![chart](https://github.com/michellejm/ConflictUrbanism_LanguageJustice/blob/master/Images/EngMono.png)

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

1. Let's do the same for answering question


## Part IV - Techniques

1. 


1. Most visualizations are both - exploratory and explanatory, but all have an exploration stage. 
2. At this point, we are going to play with the data by visualizaing it in a variety of different ways. There are 3 datasets all from the American Community Survey



 
 
 
__________________________________________________________________________________________

This tutorial was prepared by Michelle McSweeney for the Conflict Urbanism: Language Justice Course offered by the [Center for Spatial Research](http://c4sr.columbia.edu) at Columbia University in Spring 2017. 
   
