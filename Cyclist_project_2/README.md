# Case study: How does a bike-share navigate speedy success?
## Objective
The aim of this case study is to analyze customer of a fictional company, Cyclistic data from 2015 and find insight that will help the marketing team to devise new strategy to convert casual riders to annual members. The three question to guide the future marketing strategy:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy annual memberships? 
3. How can one use digital media to influence casual riders to become annual members?
## Data Source
All the data used in this case study have been provided by Google Data Analytics course on Coursera itself through multiple .zip files. Thus, this is first party data. This files have been merged to create two large .csv files.  
## Cleaning and manipulating data
Using Power Query changed all the wrong datatype in corrected format. In case of ‘starttime’ and ‘stoptime’ first split the column using delimiters then merged it and used locale the change the data type in Datetime U.S. format.
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

#### Key Insights:
1. Mode of day_of_week is 6 meaning most people using service on Saturday.
2. Average ride length of Customer is much higher than Subscriber. Probable reason:  Customer use biking service as leisure as opposed to Subscriber who use it for more practical purposes.
3. Average ride length for Customer is significantly lower compared to Subscriber on Day 6 which differs from the general pattern we see on other day .

### Detailed Analysis of usage of biking service by different user_type: 
<img width="549" height="266" alt="image" src="https://github.com/user-attachments/assets/41c57e1a-bd8b-485d-8eb3-1381b2592a3d" /> <img width="508" height="266" alt="image" src="https://github.com/user-attachments/assets/f49ff8a3-353a-48bf-b252-7c5c1d789ae5" />


#### Key Insights:
1. Day 6 or Saturday has highest count of trip. Explains why the mode of day_of_week is 6.
2. Among the users Subscriber has a occupy almost 70% while Customer occupy almost 30%. Dependent occupy the least which is neglected. 
3. Subscriber has consistently less average ride length despite such high numbers is probably because they mostly use it for commuting. High number of Subscriber also rule out being influenced by outliers.
4. Customer with less numbers of trips, significantly longer leisure trips might be the reason the average is high .

### Average ride_length on Day 6(Saturday):
Now one thing that is different from the general trend we have seen thus far is that on Day 6 avg ride length of Subscriber is much more compared to average ride length of Customer. On further investigating we learn that:
#### Customer:
Total numbers of trips on Day 6 : 87297
Total numbers of trips for on Day 6 which are more than 10 hours : 5125 (around 6%)
Total numbers of trips on Day 6 which are less than 10 hours : 82172 (around 94%)
#### Subscriber:
Total numbers of trips on Day 6 : 132897
Total numbers of trips for on Day 6 which are more than 10 hours : 56446 (around 42%)
Total numbers of trips on Day 6 which are less than 10 hours : 76451 (around 57%)
#### Key Insights:
1. Only 6% of Customer have rides longer than 10 hours compared to 42% of Subscriber, which suggest that outliers might be influencing Subscriber more than Customer.
2. To exclude outliers, let us calculate average ride_length under 10 hours for both Customers and Subscriber. We find for Customers it is 00:28:07 and Subscriber 00:12:58. Even after excluding trips more than 10 hours we see that Customer average ride length more than subscriber which align with the general pattern.
3. There may be system error for unusually long rides .

### Number of Trips vs Gender:
<img width="468" height="193" alt="image" src="https://github.com/user-attachments/assets/c49de233-742d-4ffb-9f33-6b6bc7ec8e6b" /> <img width="705" height="453" alt="image" src="https://github.com/user-attachments/assets/a5c20550-ec78-4378-a660-b6fdaaa1c551" />


Key Insights:
1. More than 75% users are male, female user accounting only around 23% .
2. The Grand Total of Trip Id in this table will differ compared to other because of missing data . 


### Number of Trips vs Age:
<img width="359" height="414" alt="image" src="https://github.com/user-attachments/assets/e3c56a57-f560-4dfd-b982-2081175c1b7d" />
<img width="845" height="433" alt="image" src="https://github.com/user-attachments/assets/b4d79d3d-20df-48aa-90cb-dfb1e91f449a" />


#### Key Insights:
1. Age groups 30-40 and 20-30 has highest share of users around 36% and 33% respectively .
2. They are followed age groups 40-50, 50-60, 60-70 around 16%, 10% and 2% respectively . Rest of them are of negligible values.
3. Basically, young working adults are mostly the users .
4. Just like previous table this one also have missing data so the Grand Total is different .

### Finding the Peak usage hour:
<img width="543" height="536" alt="image" src="https://github.com/user-attachments/assets/273a8fc3-01f7-4c0f-81eb-e147a149c0f5" />  <img width="838" height="553" alt="image" src="https://github.com/user-attachments/assets/c9290b0d-07fa-4d07-b302-c4bb4eb0eb9c" />


#### Key Insights:
1. The table filters the data according to individual trips at different starttime and only shows top 15.
2. According to table peak usage time around 17:00.
3. Peak time is around 5pm evening meaning most user finish work or school and use bikes to commute home or some other destination. It’s the evening rush hour.

### Top 20 stations users have taken ride from:
<img width="1674" height="813" alt="image" src="https://github.com/user-attachments/assets/1741153d-4cc9-4b17-8ad7-24bcef66a6d4" />

### Top 20 stations users used as destination:
<img width="1672" height="797" alt="image" src="https://github.com/user-attachments/assets/1858b18c-21eb-47a1-8ff8-6e7379a4026f" />

### Conclusion:
**1. How do annual members and casual riders use Cyclistic bikes  differently?**
* Annual members or Subscriber use bikes for commuting to work or school and back home or other practical purpose like running errands.
* Casual members or Customer who use it for leisure rides or exploration. Thus, casual members are likely to spend more time on bikes compared to annual members as supported by data.

  
**2. Why would casual riders buy Cyclistic annual memberships?**
* If Cyclistic can encourage short, frequent rides (e.g., commutes), Customers may find value in an annual membership.
* Highlighting the cost-effectiveness of membership for frequent usage compared to paying per ride can help.
* Promote membership plans emphasizing the convenience of bikes during peak commuting hours.
* Add more bikes or docking stations in areas that see high demand during these times.
* Cyclistic’s key demographic seems to be younger adults (20-39 years old), likely using bikes for commuting and recreational purposes.
* Explore strategies to make biking more appealing and accessible to older users.

  
**3. How can Cyclistic use digital media to influence casual riders to become members?**
* Targeted Campaigns: Use data to show how shorter, frequent rides can save money with a membership.
* Emphasize Benefits: Highlight perks like priority access, flat fees, and convenience for Subscribers.
* Gender Disparity: Create campaigns that highlight safety and convenience to attract more female riders.

  
**NOTE:** Need more information about financial structure of Cyclist’s subscription plan for more detailed insights.


## Dashboard
<img width="1875" height="538" alt="Screenshot 2025-12-02 140742" src="https://github.com/user-attachments/assets/e9645e25-1624-44d0-8f65-613499ba172a" />

<img width="1859" height="543" alt="Screenshot 2025-12-02 140801" src="https://github.com/user-attachments/assets/1f62ae2b-82c8-4923-982b-8bc0bcebf051" />

<img width="655" height="544" alt="Screenshot 2025-12-02 140817" src="https://github.com/user-attachments/assets/63d2fc39-b280-490e-b1ff-53906e90d1de" />

<img width="668" height="495" alt="Screenshot 2025-12-02 140839" src="https://github.com/user-attachments/assets/589c8ec6-4158-447c-aeb1-e04f3a0dcefb" />

<img width="635" height="822" alt="Screenshot 2025-12-02 140853" src="https://github.com/user-attachments/assets/1604d50d-c21b-4353-be91-791f46e8a71d" />



