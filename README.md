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

![Correlations1 gdppc](https://user-images.githubusercontent.com/114666478/201727993-3fd184b9-8cdc-44bd-844f-b7758dcc38e9.png)

PEARSON
![Correlations gdppc](https://user-images.githubusercontent.com/114666478/201728074-4b620cee-0abf-4106-b1f5-80866df451ba.png)

### The relationship between GDP and different diseases with spearman :
![Correlations1 gdp](https://user-images.githubusercontent.com/114666478/201728208-c71e2e44-8a4f-4e56-8b38-9484b927f1f8.png)

### The relationship between the year and different diseases with spearman :

![Correlations1 year](https://user-images.githubusercontent.com/114666478/201728325-66b0b58c-910c-4702-8b92-0baddabb2f92.png)

### The relationship between GDP/per capita and Alzheimer :
![Relation Alzheimer GDP percap](https://user-images.githubusercontent.com/114666478/201728441-36a697bb-4018-4b2f-ab0d-4598b577298b.png)

### The relationship between GDP/per capita and Meningitis :
![Meningitis GDP percap](https://user-images.githubusercontent.com/114666478/201728513-c5aea8ab-0e00-46ad-bf45-b1d66329796d.png)
### The distribution of per capita values of Meningitis:
![meningitis](https://user-images.githubusercontent.com/114666478/201728857-ce45ccad-256c-418a-aaf3-578e778ede3e.png)
### The full correlations of all columns with each other by Pearson and Spearman correlations:
SPEARMAN
![Full Correlations1](https://user-images.githubusercontent.com/114666478/201729029-7da5bd3e-ef89-4b42-be12-d919331623d6.png)

Pearson
![Full Correlations](https://user-images.githubusercontent.com/114666478/201729068-6a5dc447-805d-465b-b6e6-2fbcedb361b1.png)























