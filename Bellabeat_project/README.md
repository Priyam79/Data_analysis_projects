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





