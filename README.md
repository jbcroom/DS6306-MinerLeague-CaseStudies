# MSDS6306 CaseStudy1 Codebook

## MinorLeague Group Members
- Brandon Croom, Sandesh Ojha, Sangrae Cho

### Study Overview
This study contains a data analysis of two datasets `Beers.csv`
and `Breweries.csv`. The goal is to derive insights from 2,410 craft beers
from 558 breweries in the United States. 

### The Data

`data/Beers.csv`


| FEATURE   | DESCRIPTION            |
|:---------:|:---------------------:|
|Name       | The name of the beer |
|BeerID     | The unique id number of the beer|
|ABV        | Alcohol by volume of the beer   |
|IBU        | The international bitterness of the units of the beer|
|Style      | The style of the beer |
|Ounces     | Unit of measurement for the beer denoted by oz.|



`data/Breweries.csv`


|FEATURE   | DESCRIPTION   |
|:--------:|:-------------:|
| Brew_ID | The unique identification number of the brewery|
| Name    | The name of the brewery |
| City    | The city where the brewery is located|
| State   |  The State where the brewery is located ```(Limited to the U.S.)``` |


### Folder & File Information

- `CaseStudyInfo/` Contains all the background information important for understanding
the purpose of the study. This folder contains files.

  + `Case Study 01.pdf` The entire case study file that shows the list of questions being answered
  in the study.
  
- `Data/` This folder contains all the data files that is used in the study.

  + `Beers.csv` contains list of 2,410 craft beers and their respective data points
  that is measured during the study.
  + `Breweries.csv` contains information about 558 breweries  within the United States.




### The Questions

1.) How many breweries are currently present in each state?

2.) Merge beer data with the breweries data. Print the first 6 observations and the last six observations to check the merged file.

3.) Report the number of NA's in each column.

4.) Compute the median alcohol content and international bitterness unit for each state. Plot a bar chart to compare.

5.) Which state has the maximum alcoholic (ABV) beer? Which state has the most bitter (IBU) beer?

6.) What are the Summary statistics for the ABV variable?

7.) Is there an apparent relationship between the bitterness of the beer and its alcoholic content? Draw a scatter plot.

### Researcher Information & Responsibilities

| Researcher | Questions of Interest |
|:-----------:|:---------------------:|
|Brandon Croom|Data cleaning and Q1~Q7   |
|Sandesh Ojha|Presentation perp, editing code |
|Sangrae Cho|Readme, editing code|



### Session Info for the CaseStudy1


