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

