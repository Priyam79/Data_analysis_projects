# Case study: How Can a Wellness Technology Company Play It Smart?

## Objective
The aim of this case study is to analyze data from smart devices manufactured by Bellabeat, a high-tech manufacturer of health-focused products for women and use it to gain insight into how consumers are using their smart devices. The insights discovered will then help guide marketing strategy for the company. The three question to guide the future marketing strategy:
1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers? 
3. How could these trends help influence Bellabeat marketing strategy?

## Data Source
1. All the data used in this case study have been provided by Kaggle through links from Google Data Analytics course on Coursera. Thus, this is first party data.
2. All the files are in .csv format divided between two folders.

## Cleaning and manipulation of Data
1. Using Power Query Editor data format is fixed and new table containing only ID as its column so that it act as Primary key for the table to use in data modelling.
2. Data model is established using the newly created table.
3. Several other new table is created for data analyzing, one such contains aggregated (sum or mean) values corresponding to each ID.
4. New Column is created to check activity level of different users.

### Weekdays:
    ``` days_of_week = WEEKDAY('dailyActivity_merged'[ActivityDate],2) ```
### UserTypes_byTotalSteps:
    ``` UserType_byTotalSteps = SWITCH(
    TRUE(),
    'dailyActivity_merged'[TotalSteps] >= 10000, "Very Active",
    'dailyActivity_merged'[TotalSteps] >= 7500, "Fairly Active", 
    'dailyActivity_merged'[TotalSteps] >= 5000, "Lightly Active",
    "Sedentary"
    ) ``` 
### UserType_bySleep:
    ``` UserType_bySleep = SWITCH(
    TRUE(),
    'sleepDay_merged'[TotalHourAsleep]<= 6, "Poor Sleep",
    'sleepDay_merged'[TotalHourAsleep]>= 8, "Over Sleep",
     "Good Sleep") ```
### Hour:
    ``` Hour = TIME(HOUR('hourlyCalories_merged'[ActivityHour]), MINUTE('hourlyCalories_merged'[Calories]), SECOND('hourlyCalories_merged'[ActivityHour])) ```

## Analysis of Data
### TotalSteps vs Calories:
<img width="848" height="458" alt="image" src="https://github.com/user-attachments/assets/3505fa75-98d6-44c4-a08b-9dbea18a6cdb" />


* There is positive correlation between calories burned and Total number of steps.
* This is expected as number of steps increased, the distance covered increases as well also and thus more calories are burned.
* User need to be more active if they want to decrease their calories.


### Relation between sleep and minutes active:
<img width="616" height="368" alt="image" src="https://github.com/user-attachments/assets/2db51d96-d6f1-4b10-b8da-da38884b84f8" />


Fig- 1


<img width="621" height="388" alt="image" src="https://github.com/user-attachments/assets/dba87287-e9be-453a-8113-3c0d5d2fda85" />


Fig- 2


<img width="620" height="389" alt="image" src="https://github.com/user-attachments/assets/f5066c59-ccc7-445c-8d9d-f8a411fb7182" />


Fig- 3


<img width="620" height="369" alt="image" src="https://github.com/user-attachments/assets/52a5d1d1-7fec-4357-bd3a-2f7afbb96cfe" />


Fig- 4



* Fig- 1, Fig- 2, Fig- 3 and Fig- 4 are relation between TotalMinutesAsleep vs  SedentaryMinutes, LightlyActiveMinutes, FairlyActiveMinutes and VeryActiveMinutes respectively.
* From the figures it is obvious that all of them has negative correlation with TotalMinutesAsleep in the order of Sedentary > Lightly Active > Fairly Active > Very Active.
* Thus, it can be said if users want to improve their sleep, they need to be less sedentary and more active.
* More data needed to support this insight.


### Average intensity, calories and Totalsteps throughout the day:
<img width="607" height="366" alt="image" src="https://github.com/user-attachments/assets/2eaa6822-4a39-4380-ad9a-87225eb9e213" />


Fig- 1


<img width="581" height="366" alt="image" src="https://github.com/user-attachments/assets/c782ad04-9f03-452d-a21a-f050835dfcc8" />


Fig- 2


<img width="579" height="366" alt="image" src="https://github.com/user-attachments/assets/84b850e4-0ddc-488a-851d-ebb7818d8d8b" />


Fig- 3


* Fig-1, Fig-2 and Fig-3 shows relation between daily time and calories , total steps and total intensity respectively.
* Avg steps increases from 7:00 to 12:00 and again from 16:00 to 19:00 showing that people are most active during this time.
* Calories and average intensity also follows same trends as total steps.


### Usertype by Sleep, minutes and Totalsteps:
<img width="566" height="451" alt="image" src="https://github.com/user-attachments/assets/b2995eb5-d826-475f-bc3f-54dbc4177d9c" />


<img width="589" height="451" alt="image" src="https://github.com/user-attachments/assets/2f9e9bd6-2679-48c8-b1d7-75436d0e5fc6" />

  
<img width="602" height="451" alt="image" src="https://github.com/user-attachments/assets/c6359487-161f-42a7-8253-9da42467fb4a" />


* 58% of user have poor sleep(less than 6 hours) while only 33% have good sleep(between 6-8 hours).
* 36%(12 users) of user are very active, while 24%(8 users) are lightly active and 21%(7 users) are fairly active. Only 18%(6 users) are sedentary.  
* 21%(7 users) have more than 10000 steps (very active), 27%(9 users) have steps between 7500 and 10000 (fairly active), 27%(9 users) have steps between 5000 and  7500 (lightly active) and 24%(8 users) have less than 5000 steps (sedentary). 


### Sleep pattern for different usertype:
<img width="873" height="544" alt="image" src="https://github.com/user-attachments/assets/25dbafc3-7437-4e0c-a1fb-8c2c9d40d6a5" />


* Through the visuals it is clear that sedentary group has the worst sleepers and as activity increases, we see better sleep pattern. 
* Over sleepers decreases as activity level increases as more active users will spend less amount of time staying in bed.
* More data required as it seems very active user have more poor sleepers than normal sleepers but that could be because of missing data and smaller sample dataset.


### Conclusion

**1. Daily notification on steps and posts on app:**
The data shows the positive correlation between calories and steps. Thus, we can encourage users to take the recommended 7500 steps everyday by using notification when they are not meeting daily quota.

**2. Notification and sleep techniques:**
Based on result most users are not getting the recommended hours of sleep i.e. 6-8 hours . Encourage users to get proper sleep by using notification and post explaining why good sleep is required.

**3. Daily use of smart device:**
More than 50% users are either active or fairly active on the smart users. Thus, the device need to be more durable, water resistant and light. For other users we need to promote by they should use it more by giving more features to make it more usable in daily life.
 
**4. Reward system:**
Most users might not get motivated by just notification so maybe there should be reward system to encourage them should they consistently reach their daily goal.


## Dashboard


<img width="1062" height="591" alt="Screenshot 2025-12-03 003012" src="https://github.com/user-attachments/assets/72659bcd-5941-4317-9037-3996bbab0ce0" />


