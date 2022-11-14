# Proyecto-ETL
![main_928px](https://user-images.githubusercontent.com/114666478/201599140-5343ab95-96b7-4baf-aacd-6c9a2dc09975.jpg)

## Theme of the Project:
#### Exploration of the relationship and correlations between different diseases and both the countries gdp as well as its gdp per capita.
## Needs of the Project:
#### Database with total frequency of each illness per country per year as well as population numbers per country per year and economic indicators.

## Steps:
### Extract (3 sources and 2 methods)
### Transform 
### Load to a Database
### Interpret the results


## Extraction:
### First Source:
#### https://www.kaggle.com/datasets/iamsouravbanerjee/cause-of-deaths-around-the-world
#### Download CSV file, read with pandas. 
#### This dataframe is the base df with which to combine the additional information needed.

### Second Source:
#### http://www.geoba.se/population.php?pc=world&type=28&year=1990&st=country&asde=&page=3
#### Scrapping will be necessary, 60 different links with 400 datapoints per link
#### First attempt with selenium and parallelization is too slow, change methods to only parallelized beautifulsoup possible due to the url being consistent
#### Optimized code to increase speed as much as possible, full extraction takes 45 minutes.

### Third Source:
#### https://en.wikipedia.org/wiki/List_of_countries_by_past_and_projected_GDP_(nominal)
#### Scrapping with Instant Data scraper viable due to few pages needed.
#### Download CSV file and read in pandas

### Issues during Extraction:
#### Scrapping and creating pandas dataframes from the data was extremely slow, even with beautifulsoup. Initially the scrapping was done but due to inconsistent data structure no dictionary was created. Each debugging took around half an hour even when only loading half the datapoints.


![Captura](https://user-images.githubusercontent.com/114666478/201597872-58382775-00a9-4b23-9fc4-36acfc5c6343.PNG)


#### Instant data scrapping was inconsistent with both Country names as well as column tags.

## Transformation

### Cleaning by sources:
#### No Cleaning is necessary for the first CSV source from Kaggle
#### After the first scrapping, we have a list of 60 data frames, we join the data frames by year.  We also remove the commas from the population numbers and convert the datatypes to integers. We save all the separate data frames and create a new common data frame sorted by country name, all_sort. We modify an error in the database and switch 2018 by 2019 in the second appearance
#### We now merge the first two tables by normalizing the point at which they are going to be joined. This will create null values due to the number of countries in each dataset being different. we name this new data frame data_int
#### We create a null value column in this new data frame and remove all rows with more than 3 nulls (thus removing all inconsistent countries)
#### A per capita column is created for each disease column, with the value in each row of the total incidence divided by the value in each row of the population, thus creating a per capita frequency, we will only be using this further on as it is the only relevant metric.
#### Now we are transforming the economic numbers, we first remove the nulls either by adding additional information from the internet or removing outright when not relevant(south Sudan) Any economic data we cannot get we also fill with the economic year of the previous years.
#### We now create a differentiated data frame that contains the columns: country, year, and economy so that we can normalize it with the other data frames and get a data frame with the same shape. We do that by creating a list of dictionaries.
#### For the second economic dataset we have to do the same processes with an additional step of renaming columns due to data scrapping issues
#### We now concatenate both economic datasets into a single combined data frame of all economic data by country by year from 2000-2019
#### We again normalize all column names and merge it into our previous finished data frame of data_int, now we have all data sorted and normalized, we again drop nulls that could originate from an unequal number of countries in both data frames.
#### We create a gdp/percap column containing all gdp per capita calculations for each country in each year

##Load
#### We load all necessary data frames to SQL, due to the transformation already having been done no further work is needed on SQL

##Insights
#### We set up three correlation tables (Pearson, spearman, and Kendall) and apply them to create relationships between the factors that are interesting

### The relationship between GDP/per capita and different diseases with Pearson and spearman :
SPEARMAN





















