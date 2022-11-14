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


















