# Case study: How does a bike-share navigate speedy success?
## Objective
The aim of this case study is to analyze customer of a fictional company, Cyclistic data from 2015 and find insight that will help the marketing team to devise new strategy to convert casual riders to annual members. The three question to guide the future marketing strategy:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy annual memberships? 
3. How can one use digital media to influence casual riders to become annual members?
## Data Source
All the data used in this case study have been provided by Google Data Analytics course on Coursera itself through multiple .zip files. Thus, this is first party data. This files have been merged to create two large .csv files.  
## Cleaning and manipulating data
Using Power Query changed all the wrong datatype in corrected format. Incase of ‘starttime’ and ‘stoptime’ first split the column using delimiters then merged it and used locale the change the data type in Datetime U.S. format.
Created new columns such as ‘ride_length’, ‘day_of_week’, ‘age’, ‘timing_of_starttime’ .
Missing data mostly neglected .
Also a age bin created . 
### ride_length
```
ride_length = 
VAR Total_Seconds = ABS(DATEDIFF(Divvy_Trips_2015_Q1Q2[stoptime], Divvy_Trips_2015_Q1Q2[starttime], SECOND))
VAR Total_Hours = INT(Total_Seconds / 3600)
VAR Total_Minutes = INT(MOD(Total_Seconds, 3600) / 60)
VAR Total_Seconds_Remaining = MOD(Total_Seconds, 60)
RETURN
    FORMAT(Total_Hours, "00") & ":" & FORMAT(Total_Minutes, "00") & ":" & FORMAT(Total_Seconds_Remaining, "00")

```
### day_of_week
``` Days_of_week = WEEKDAY(Divvy_Trips_2015_Q1Q2[starttime],2)```
### Age
```Age = 2015 - Divvy_Trips_2015_Q1Q2[birthyear] ```
### timing_of_starttime
```TimeOnly = TIME(HOUR('Divvy_Trips_2015_Q1Q2'[starttime]), MINUTE('Divvy_Trips_2015_Q1Q2'[starttime]), SECOND('Divvy_Trips_2015_Q1Q2'[starttime]))```
## Analysis of Data
### Average ride_length vs Day_of_week summarize
<img width="1226" height="309" alt="image" src="https://github.com/user-attachments/assets/d9244e82-8107-4a6f-817d-c6ec44b15e3a" />
<img width="415" height="216" alt="image" src="https://github.com/user-attachments/assets/f39e566a-a060-4bc6-a64f-e96270cd8406" />
The above table is a summarized version of average ride_length which is the average duration of a ride from start to finish, on different day of week that is from Monday to Sunday where Monday is represented as 1, Tuesday as 2 and so on ending with Sunday as 7. 

Key Insights:
Mode of day_of_week is 6 meaning most people using service on Saturday.
Average ride length of Customer is much higher than Subscriber. Probable reason:  Customer use biking service as leisure as opposed to Subscriber who use it for more practical purposes.
Average ride length for Customer is significantly lower compared to Subscriber on Day 6 which differs from the general pattern we see on other day

