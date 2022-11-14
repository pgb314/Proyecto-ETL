# Proyecto-ETL

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
#### First attempt with selenium and parallelization is too slow, change methods to only beautifulsoup possible due to the links url being consistent
#### Optimized code to increase speed as much as possible, full extraction takes 45 minutes.

### Third Source:
#### https://en.wikipedia.org/wiki/List_of_countries_by_past_and_projected_GDP_(nominal)
#### Scrapping with Instant Data scraper viable due to few pages needed.
#### Download CSV file and read in pandas


