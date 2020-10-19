# *Lab 1*  
  

**Contents**:  

* 1) [Data Preparation and Manipulation](#data-preparation-and-manipulation)      
* 2) [Analysis of Daily New Corona Cases and Deaths](#analysis-of-daily-new-corona-cases-and-deaths)    
* 3) [Preparing and Analyzing the World Bank Data](#preparing-and-analyzing-the-world-bank-data)
* 4) [Joining the Datasets](#joining-the-datasets)  

The John's Hopkins Novel Corona Virus (COVID-19) epidemiological data is compiled by the Johns Hopkins University Center for Systems Science and Engineering (JHU CCSE) from various sources. <br>
The dataset contains data since 22nd of January 2020.


### Data Preparation and Manipulation   

1. We first prepare and aggregate the data.   
a. load the `Corona Confirmed Cases Narrow`, the `Corona Confirmed Deaths Narrow`, and the `Corona Confirmed Recovered Narrow` datasets directly from the John's Hopkins website. 

b. Create new data-frames named `cases.agg`, `deaths.agg`, and `recovered.agg` which aggregate the `sum` of Corona cases, deaths, and recovered respectively over the different countries' provinces.     

c. using `tidyverse`. 

d. Using the last day of March as a reference, create a single stacked bar-plot that visualizes the top 10 countries in terms of their Corona cases, and their respected Corona deaths and recovered cases stacked on top of the current sick people. 

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/000005.png)

What is the biggest issue with the information presented in this plot? 
The issue of this plot is that it doesnt show the proportion of the cases to the population. so we cant compere the effect of the apidemic on the state to the othe countries.



### Analysis of Daily New Corona Cases and Deaths  

The two datasets (Corona Cases and Deaths) register the value of cases and deaths, respectively, as a cumulative sum for each day.

a. Add `Diff` to both the `cases.agg` and the `deaths.agg` data-frames. This new column should register the daily `Value` difference for each country. In other words, the `Diff` column shows how many new cases/deaths each country incurs every day.  

b. Find the top 10 instances of country and date combinations with the greatest absolute number of new daily Corona cases and deaths (separately).

c. Italy's new daily Corona cases AND deaths as a function of Date.
![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/000023.png)

d.logarithm scale.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/000027.png)



### Preparing and Analyzing the World Bank Data   

a. Rename the columns of `eco_data`

b. Create a new `eco` data-frame whose dimensions are $N \times 11$, where `N` is the number of countries. 
The columns should be the features with their respective values in eco_data for each country from 2018. 

c. Select and rename the following columns: `country` as country, `GDP(US currency)` as GDP, `Population ages 65 and above (% of total population)` as pop65, `Population in the largest city (% of urban population)` as pop_city_ratio, `Population, total` as pop_total columns . 

d. The % of population over 65 vs. log of GDP per capita in 2018, after excluding the 10% countries with the lowest GDP per capita. Using `lm` and `abline`, add a regression line to the plot.

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/000022.png)



### Joining the Datasets   

a. Join the `deaths.agg`, `cases.agg`, and `recovered.agg` into one data-frame called `corona`.

b. Join the `corona` and `eco` data-frames in a way that will keep the most information regarding the data .   

c. New columns of normalized `cases`, `deaths`, and `recovered` so they will show the number of cases per 100,000 people for each country.   
 
d. Using the last day of March as a reference, create a scatter-plot of normalized deaths and cases vs. `pop65`. Limit the plot to show only countries with 15% or more of `pop65`.   
--- outliers( pop65>24, norm100K_deaths>15) in that plot in red and add to the plot their country names

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/000005s.png)

![alt text](https://github.com/chencnaani/Data-Analysis-with-R/blob/master/00000aa.png)

