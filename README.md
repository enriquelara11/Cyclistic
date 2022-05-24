### Enriuqe Lara's Porfolio

# Google Data Analytics Capstone Project: Cyclistic Bike-share Analysis
Cyclistic is a Chicago-based bike sharing company. The firm operates a bike-sharing program with about 5,800 bikes and 600 docking stations located across the city. Cyclistic makes bike-sharing more accessible to those with disabilities by providing reclining bikes, hand tricycles, and cargo bikes. The comapny started a successful bike-sahring service in 2016 and since then, the firm has grown to over 5200 bicycles that are geotracked and linked to a network of over 620 stations across Chicago. So far the company has relied on building general awareness and appealing to customer segments. With options for single-day passes, full-day passes, and yearly memberships, pricing flexibility has been a cornerstone of the company's success. Annual memberships, according to our Director of Marketing, will be the key to future growth.

### Scenario
You are a junior data analyst working for the marketing analyst team for Cyclistic. The Director of Marketing Lily Moreno believes that annual memeberships are the key to future success for the company. Your team wants the understand the differences between how casual and annual memebers use the cyclistic bike-sharing program. Using these insights your team will make a recommendation to convert casual riders to annual members. The information provided needs to be compelling filled with strong visuals in order for the executives at cyclistic to approve it. 

Moreno has asked you to ansers the first question: How do annual members and casual riders use Cyclistic bikes diﬀerently?


### Business Task
Identify the difference between our casual and annual riders. We'll be on the lookout for patterns and clues as to what distinguishes the two groups. We will give recommendations based on our findings on how to raise the number of annual members. Our marketing staff will then be informed of our results.

### Stakeholders
- Director of Marketing: Lily Moreno
- Cyclistic Marketing Analytics Team (my team)
- Cyclistic Executive Team 

### Data
Special thank you to Motivate International Inc. for providing the following data:
[Cyclistic Trip Data](https://divvy-tripdata.s3.amazonaws.com/index.html)
- The data seems trustworthy, and the time period appears to correspond to the proper dates and times.
- Data is understandable and reasonable

### Data Limitation
Upon further review of the data some of the data some of the start_station_name, start_station_id, end_station_name, end_station_id variables had missing values. These missing values are important to the overall anal 

## Cleaning our Data
We begin by installing/loading the required libraries for our analysis. 
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
We will import our 12 .csv files. Each of the files represents a month of the year.
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
###Prepare the data:
In this step we will prepare the data for analysis. We will combine the data into one single data frame, convert the dates and time to timestamps wihtin R, and finally remove any empty rows if any.
```{r}
#Data Cleaning 
### Combining the different data files
bike_rides <- rbind(df1, df2, df3, df4, df5, df6, df7, df8, df9, df10, df11, df12)

### Using the lubridate function to convert start date and end date to TIMESTAMPS
bike_rides$started_at <- lubridate::mdy_hm(bike_rides$started_at)
bike_rides$ended_at <- lubridate::mdy_hm(bike_rides$ended_at)

### also using lubridate to convert ride_length to time stamps as well
bike_rides$ride_length <- lubridate::hms(bike_rides$ride_length)

### Removing any empty rows
bike_rides %>%
  remove_empty()

```




### Conclusion
Based on our analysis we discovered that annual and causual riders differ in the way in which they ride our bikes. Casuals tend to be more impulsive, enthusiastic about riding near the city's coast and skyline while annual members appear to be motivated, living on a consistent schedule, and riding our bike for sport.


From our analysis we have draw 3 recommendations we believe can be effective at converting casual riders into annual members: 
1. Target casuals with specified advertisements. Emphasize the distinguising characteristics of the memership. Health and excercise for exmaple are two topics that could be promoted.
2. Increase the initial fee that casual riders pay for riding. We may be able to persuade people who are on the fence about switching using this strategy by making the annual membership more appealing.
3. We could breakup the membership. Different needs for different people. From our analysis we can see differences between annual and casual riders, so we could create a memebership that is appealing for a larger group of customers. A seasonal membership could be one example.



Thank you for looking at my project! I hope you enjoyed it as much as I did!



