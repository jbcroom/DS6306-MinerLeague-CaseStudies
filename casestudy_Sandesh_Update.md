---
title: "Case_Study_1 Update"
author: "Sandesh Ojha"
date: "June 19, 2019"
output: 
  html_document:
    keep_md: TRUE
---



```r
#install necessary libraries
library(dplyr)
library(ggplot2)

#Setup the environment for working
WorkingDirPath = "C:/Users/sojha.WVOFFICE.000/Documents/SMU/Summer 2019/Doing Data Science/CaseStudy1_2_2_2"
setwd(WorkingDirPath)
beerFile = "Beers.csv"
breweryFile = "Breweries.csv"

#Read the files into dataframes
beerDF = read.csv(beerFile)
breweryDF = read.csv(breweryFile)
```

####Question 1 : How many breweries are present in each state?

```r
#Counting the number of breweries by state
brewerysByState = breweryDF %>% count(State,sort=TRUE)
names(brewerysByState) = c("State", "Count")
print(brewerysByState,n=51)
```

```
## # A tibble: 51 x 2
##    State Count
##    <fct> <int>
##  1 " CO"    47
##  2 " CA"    39
##  3 " MI"    32
##  4 " OR"    29
##  5 " TX"    28
##  6 " PA"    25
##  7 " MA"    23
##  8 " WA"    23
##  9 " IN"    22
## 10 " WI"    20
## 11 " NC"    19
## 12 " IL"    18
## 13 " NY"    16
## 14 " VA"    16
## 15 " FL"    15
## 16 " OH"    15
## 17 " MN"    12
## 18 " AZ"    11
## 19 " VT"    10
## 20 " ME"     9
## 21 " MO"     9
## 22 " MT"     9
## 23 " CT"     8
## 24 " AK"     7
## 25 " GA"     7
## 26 " MD"     7
## 27 " OK"     6
## 28 " IA"     5
## 29 " ID"     5
## 30 " LA"     5
## 31 " NE"     5
## 32 " RI"     5
## 33 " HI"     4
## 34 " KY"     4
## 35 " NM"     4
## 36 " SC"     4
## 37 " UT"     4
## 38 " WY"     4
## 39 " AL"     3
## 40 " KS"     3
## 41 " NH"     3
## 42 " NJ"     3
## 43 " TN"     3
## 44 " AR"     2
## 45 " DE"     2
## 46 " MS"     2
## 47 " NV"     2
## 48 " DC"     1
## 49 " ND"     1
## 50 " SD"     1
## 51 " WV"     1
```

```r
#Ploting the number of breweries in each state to provide a visual output
ggplot(data=brewerysByState, aes(x=reorder(State,Count), y=Count, fill=State)) + geom_bar(stat="identity", show.legend = FALSE) + labs(x ="State",y="Brewery Count",title="Number of Breweries by State") + theme(plot.title = element_text(size = 16,face= "bold",hjust = 0.5)) + theme(axis.text = element_text(size=8),axis.title=element_text(size=10))
```

![](casestudy_Sandesh_Update_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

####Question 2 : Merge beer data with the breweries data.  Print the first 6 observations and the last six observations to check the merged file.

```r
#Merging the beer and breweries data into a new data frame
BeersAndBreweriesDF = merge(x=beerDF,y=breweryDF,by.x="Brewery_id",by.y="Brew_ID")
head(BeersAndBreweriesDF,6)
```

```
##   Brewery_id        Name.x Beer_ID   ABV IBU
## 1          1  Get Together    2692 0.045  50
## 2          1 Maggie's Leap    2691 0.049  26
## 3          1    Wall's End    2690 0.048  19
## 4          1       Pumpion    2689 0.060  38
## 5          1    Stronghold    2688 0.060  25
## 6          1   Parapet ESB    2687 0.056  47
##                                 Style Ounces             Name.y
## 1                        American IPA     16 NorthGate Brewing 
## 2                  Milk / Sweet Stout     16 NorthGate Brewing 
## 3                   English Brown Ale     16 NorthGate Brewing 
## 4                         Pumpkin Ale     16 NorthGate Brewing 
## 5                     American Porter     16 NorthGate Brewing 
## 6 Extra Special / Strong Bitter (ESB)     16 NorthGate Brewing 
##          City State
## 1 Minneapolis    MN
## 2 Minneapolis    MN
## 3 Minneapolis    MN
## 4 Minneapolis    MN
## 5 Minneapolis    MN
## 6 Minneapolis    MN
```

```r
tail(BeersAndBreweriesDF,6)
```

```
##      Brewery_id                    Name.x Beer_ID   ABV IBU
## 2405        556             Pilsner Ukiah      98 0.055  NA
## 2406        557  Heinnieweisse Weissebier      52 0.049  NA
## 2407        557           Snapperhead IPA      51 0.068  NA
## 2408        557         Moo Thunder Stout      50 0.049  NA
## 2409        557         Porkslap Pale Ale      49 0.043  NA
## 2410        558 Urban Wilderness Pale Ale      30 0.049  NA
##                        Style Ounces                        Name.y
## 2405         German Pilsener     12         Ukiah Brewing Company
## 2406              Hefeweizen     12       Butternuts Beer and Ale
## 2407            American IPA     12       Butternuts Beer and Ale
## 2408      Milk / Sweet Stout     12       Butternuts Beer and Ale
## 2409 American Pale Ale (APA)     12       Butternuts Beer and Ale
## 2410        English Pale Ale     12 Sleeping Lady Brewing Company
##               City State
## 2405         Ukiah    CA
## 2406 Garrattsville    NY
## 2407 Garrattsville    NY
## 2408 Garrattsville    NY
## 2409 Garrattsville    NY
## 2410     Anchorage    AK
```

```r
#Cleanup the names of the columns to make the data more understandable
names(BeersAndBreweriesDF) = c("Brewery_id","Beer_Name","Beer_ID","ABV","IBU","Beer_Style","Beer_OZ","Brewery_Name","Brewery_City","Brewery_State")
```

####Question 3 : Report the number of NA's in each column.

```r
sapply(BeersAndBreweriesDF, function(x) sum(is.na(x)))
```

```
##    Brewery_id     Beer_Name       Beer_ID           ABV           IBU 
##             0             0             0            62          1005 
##    Beer_Style       Beer_OZ  Brewery_Name  Brewery_City Brewery_State 
##             0             0             0             0             0
```

####Question 4 : Compute the median alcohol content and international bitterness unit for each state.  Plot a bar chart to compare.

```r
#Calculating the median ABV and median IBV by state. Ignoring missing values
ABVByState = BeersAndBreweriesDF %>% group_by(Brewery_State) %>% summarise(median=median(ABV,na.rm=TRUE))
IBUByState = BeersAndBreweriesDF %>% group_by(Brewery_State) %>% summarise(median=median(IBU,na.rm=TRUE))

#Cleanup the dataframe names
names(ABVByState) = c("State","MedianABV")
names(IBUByState) = c("State","MedianIBU")



#Bar charts for comparison
#ABVByState
 ggplot(data=ABVByState, aes(x=reorder(State,MedianABV), y=MedianABV, fill=State)) + geom_bar(stat="identity", show.legend = FALSE) + labs(x ="State",y="ABV",title="ABV by State") + theme(plot.title = element_text(size = 16,face= "bold",hjust = 0.5)) + theme(axis.text = element_text(size=8),axis.title=element_text(size=10))
```

![](casestudy_Sandesh_Update_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
#IBUByState
  ggplot(data=IBUByState, aes(x=reorder(State,MedianIBU), y=MedianIBU, fill=State)) + geom_bar(stat="identity", show.legend = FALSE) + labs(x ="State",y="IBU",title="IBU by State") + theme(plot.title = element_text(size = 16,face= "bold",hjust = 0.5)) + theme(axis.text = element_text(size=8),axis.title=element_text(size=10))
```

![](casestudy_Sandesh_Update_files/figure-html/unnamed-chunk-5-2.png)<!-- -->


####Question 5 : Which state has the maximum alcoholic(ABV) beer? Which state has the most bitter (IBU) beer ?


```r
 #Filter the data to get the single row with maximum ABV
 maxABVStateDF = BeersAndBreweriesDF %>% filter(ABV == max(ABV,na.rm=TRUE))
 
 #Put just the Brewery State in a vector
 maxABVState = maxABVStateDF$Brewery_State[1]
 as.character(maxABVState)
```

```
## [1] " CO"
```

```r
 #Filter the data to get the single row with maximum IBU
 maxIBUStateDF = BeersAndBreweriesDF %>% filter(IBU ==   max(IBU,na.rm=TRUE))
 
 #Put just the Brewery State in a vector
 maxIBUState = maxIBUStateDF$Brewery_State[1]
 as.character(maxIBUState)
```

```
## [1] " OR"
```

####Question 6 : Summary Statistics for the ABV variable.

```r
 #summary statistics for the ABV variable
 summary(BeersAndBreweriesDF$ABV)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
## 0.00100 0.05000 0.05600 0.05977 0.06700 0.12800      62
```

####Question 7 : Is there an apparent relationship between the bitterness of the beer and it's alcholic content? Draw a scatter plot.


```r
#Scatter plot of bitterness (IBU) and alcoholic content (ABV)
ggplot(BeersAndBreweriesDF, aes(x=ABV, y=IBU)) + geom_point()
```

```
## Warning: Removed 1005 rows containing missing values (geom_point).
```

![](casestudy_Sandesh_Update_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
 
Github - https://github.com/jbcroom/DS6306-MinerLeague-CaseStudies
 
