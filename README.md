# Google Data Analytics Capstone Project: Cyclistic Bike-share Analysis
Presented by Enrique Lara

This is my capstone project for the Google Data Analytics Proffesional Certificate, hope you guys enjoy!

## Introduction and Overview of our Scenario
Cyclistic is a Chicago-based bike sharing company. The firm operates a bike-sharing program with about 5,800 bikes and 600 docking stations located across the city. Cyclistic makes bike-sharing more accessible to those with disabilities by providing reclining bikes, hand tricycles, and cargo bikes. The comapny started a successful bike-sahring service in 2016 and since then, the firm has grown to over 5200 bicycles that are geotracked and linked to a network of over 620 stations across Chicago. So far the company has relied on building general awareness and appealing to customer segments. With options for single-day passes, full-day passes, and yearly memberships, pricing flexibility has been a cornerstone of the company's success. Annual memberships, according to our Director of Marketing, will be the key to future growth.

You are a junior data analyst working for the marketing analyst team for Cyclistic. The Director of Marketing Lily Moreno believes that annual memeberships are the key to future success for the company. Your team wants the understand the differences between how casual and annual memebers use the cyclistic bike-sharing program. Using these insights your team will make a recommendation to convert casual riders to annual members. The information provided needs to be compelling filled with strong visuals in order for the executives at cyclistic to approve it. 

Moreno has asked you to ansers the first question: How do annual members and casual riders use Cyclistic bikes diﬀerently?

### Stakeholders
- Director of Marketing: Lily Moreno
- Cyclistic Marketing Analytics Team (my team)
- Cyclistic Executive Team 

### Business Task
Our goal is to dentify the difference between our casual and annual riders. We'll be on the lookout for patterns and clues as to what distinguishes the two groups. We've been tasked with developing recommendations based on our results for increasing the number of annual members. The results will then be shared with our marketing team.

## Our Data
Special thank you to Motivate International Inc. for providing the following data:
[Cyclistic Trip Data](https://divvy-tripdata.s3.amazonaws.com/index.html) under the following [license](https://ride.divvybikes.com/data-license-agreement).

We will be using the "ROCCC" method to determine the credibility and integrity of the data.
- Reliability: The data is trustworthy, and the data has a consistent structure across several datasets. The information comes from Lyft Bikes and Scooters, LLC, the City of Chicago, and the Divvy service provider.
- Orginality: Motivate International Inc. and the city of Chicago offer the data, which are credible sources.
- Comprehensiveness: The data is well-understood, and each of the dataset's factors makes sense.
- Current: Dates in the data are current, we examined datsets for each month of the year 2021.
- Cited: The data is cited under the license aggreement.


### Limits in our Data
Upon further review of the data we can see that there are some missing values in the columns "start_station_name", "start_station_id", "end_station_name", "end_station_id".

While the missing values may have an impact on our overall analysis, we feel we have enough data to compensate for any bias introduced by such missing values. 

### Cleaning our Data
Cleaning our data is an important step in the Data Analysis process since it eliminates flaws that could render our data useless.

> We begin by installing/loading the required libraries for our analysis:
```{r}
## Required Libraries
library(tidyverse)
library(lubridate)
library(janitor)
library(readxl)
library(dplyr)
library(scales) 
library(ggplot2)
library(Rserve)
library(RColorBrewer)
library(chron)
```
> We move on to importing the required files to our working enviroment in R. In this case we have 12 CSV files, each representing a month of the year for 2021.
```{r}
##Importing the csv files into new data frames
df1 <- read_csv("202101-divvy-tripdata.csv")
df2 <- read_csv("202102-divvy-tripdata.csv")
df3 <- read_csv("202103-divvy-tripdata.csv")
df4 <- read_csv("202104-divvy-tripdata.csv")
df5 <- read_csv("202105-divvy-tripdata.csv")
df6 <- read_csv("202106-divvy-tripdata.csv")
df7 <- read_csv("202107-divvy-tripdata.csv")
df8 <- read_csv("202108-divvy-tripdata.csv")
df9 <- read_csv("202109-divvy-tripdata.csv")
df10 <- read_csv("202110-divvy-tripdata.csv")
df11 <- read_csv("202111-divvy-tripdata.csv")
df12 <- read_csv("202112-divvy-tripdata.csv")
```
### Preparing our data for analysis
Preparing our data is essential for making it efficient and accessible to others. We'll use R to modify our data because of its rich visualization capabilities and statistical analysis, both of which are critical for our analysis.

> To work better with our data, we need to consolidate and create one single data frame, we will be using the Rbind function in R to perform the task.
```{r}
### Combining the different data files
bike_rides <- rbind(df1, df2, df3, df4, df5, df6, df7, df8, df9, df10, df11, df12)
```
> We'll utilize the Lubridate function to create a consistent date format because our data contains dates that aren't easily rocongized by R.
```{r}
### Using the lubridate function to convert start date and end date to TIMESTAMPS
bike_rides$started_at <- lubridate::mdy_hm(bike_rides$started_at)
bike_rides$ended_at <- lubridate::mdy_hm(bike_rides$ended_at)

### also using lubridate to convert ride_length to time stamps as well
bike_rides$ride_length <- lubridate::hms(bike_rides$ride_length)
```
> We will remove any empty rows in our dataset using the following operation.
```{r}
### Removing any empty rows
bike_rides %>%
  remove_empty()
```
Further anlaysis of our project can be reviewed here [Cyclist_R_Markdown.Rmd](https://github.com/enriquelara11/Cyclistic/blob/main/Cyclist_R_Markdown.Rmd).




## Analyze
Based on our analysis we discovered that annual and causual riders differ in the way in which they ride our bikes. Casuals tend to be more impulsive, enthusiastic about riding near the city's coast and skyline while annual members appear to be motivated, living on a consistent schedule, and riding our bike for sport.


From our analysis we have draw 3 recommendations we believe can be effective at converting casual riders into annual members: 
1. Target casuals with specified advertisements. Emphasize the distinguising characteristics of the memership. Health and excercise for exmaple are two topics that could be promoted.
2. Increase the initial fee that casual riders pay for riding. We may be able to persuade people who are on the fence about switching using this strategy by making the annual membership more appealing.
3. We could breakup the membership. Different needs for different people. From our analysis we can see differences between annual and casual riders, so we could create a memebership that is appealing for a larger group of customers. A seasonal membership could be one example.

## Share
I was able to develop a presentation where I could convey all of my findings utilizing visuals created in R and some in Tableau. I'm happy to share my creation with you via this link.


Thank you for looking at my project! I hope you enjoyed it as much as I did!



