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
'''ride_length_mins = ABS(DATEDIFF(Divvy_Trips_2015_Q1Q2[stoptime],Divvy_Trips_2015_Q1Q2[starttime],MINUTE))'''
