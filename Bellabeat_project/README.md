## Case Study: How Can a Wellness Technology Company Play It Smart?

## Objective
The aim of this case study is to analyze data from smart devices manufactured by Bellabeat, a high-tech manufacturer of health focused products for women and use it to gain insight into how consumers are using their smart devices. The insights discovered will then help guide marketing strategy for the company. The three question to guide the future marketing strategy:

• What are some trends in smart device usage?

• How could these trends apply to Bellabeat customers? 

• How could these trends help influence Bellabeat marketing strategy?

## Data Source
All the data used in this case study have been provided by Google Data Analytics course on Coursera itself through multiple .zip files. Thus, this is first party data. This files have been merged to create two large .csv files.

## Cleaning and Manipulating Data
Using Power Query changed all the wrong datatype in corrected format. Missing data were neglected. After modelling the data  new columns and measures were added as and when required. In table *dailyActitvity_merged* we create the following columns:

``` days_of_week = WEEKDAY('dailyActivity_merged'[ActivityDate],2) ```

```
UserType_byTotalSteps = SWITCH(
    TRUE(),
    'dailyActivity_merged'[TotalSteps] >= 10000, "Very Active",
    'dailyActivity_merged'[TotalSteps] >= 7500, "Fairly Active", 
    'dailyActivity_merged'[TotalSteps] >= 5000, "Lightly Active",
    "Sedentary"
)
```

*days_of_week* converts dates into corresponding dates to its weekdays. *UserType_byTotalSteps* bins users in three categories by number of steps they have taken. Others calculations including extracting time from datetime columns and calculating sleep hours.

```Hour = TIME(HOUR('hourlyCalories_merged'[ActivityHour]), MINUTE('hourlyCalories_merged'[Calories]), SECOND('hourlyCalories_merged'[ActivityHour])) ```

This calculated column is created in multiple tables.

```TotalHourAsleep = 'sleepDay_merged'[TotalMinutesAsleep] / 60 ```

Other calculated columns includes categorising users in 3 groups according to their sleep patterns

```
UserType_bySleep = SWITCH(
    TRUE(),
    'sleepDay_merged'[TotalHourAsleep]<= 6, "Poor Sleep",
    'sleepDay_merged'[TotalHourAsleep]>= 8, "Over Sleep",
     "Good Sleep")
```

## Analysis of Data
### TotalSteps vs Calories:

<img width="682" height="367" alt="image" src="https://github.com/user-attachments/assets/a01d604b-95c4-4f93-b381-c09eea079647" />

• There is positive correlation between calories burned and Total number of steps.

• This is expected as number of steps increased, the distance covered increases as well also and thus more 
calories are burned.

• User need to be more active if they want to decrease their calories.

### Relation between sleep and minutes active:

<img width="492" height="346" alt="Screenshot 2025-12-25 221623" src="https://github.com/user-attachments/assets/93bbf008-f8ae-4775-bfc5-1e5ff5c3a468" />

<img width="494" height="372" alt="Screenshot 2025-12-25 221637" src="https://github.com/user-attachments/assets/7ecdfb4e-5714-4ba9-86dc-6f7daef4931b" />

<img width="491" height="364" alt="Screenshot 2025-12-25 221703" src="https://github.com/user-attachments/assets/88ba693e-112f-4ef0-bc02-728b54eaeb77" />

<img width="489" height="356" alt="Screenshot 2025-12-25 221736" src="https://github.com/user-attachments/assets/bfea2eec-3a1d-4311-b5d6-005afa9161c8" />

• Fig-1, Fig-2, Fig-3 and Fig-4 are relation between TotalMinutesAsleep vs  SedentaryMinutes, LightlyActiveMinutes, FairlyActiveMinutes and VeryActiveMinutes respectively.

• From the figures it is obvious that all of them has negative correlation with TotalMinutesAsleep in the order of Sedentary > Lightly Active > Fairly Active > Very Active.

• Thus, it can be said if users want to improve their sleep, they need to be less sedentary and more active.

• More data needed to support this insight.

### TotalSteps per Weekday:

<img width="706" height="442" alt="image" src="https://github.com/user-attachments/assets/1e46d0b6-905f-4bf6-b0a9-9998f2053d8a" />

 Users walk daily the recommended number of steps of 7500 besides Thursday, Friday and Sunday.

 ### Average intensity, calories and Totalsteps throughout the day:

<img width="1064" height="274" alt="Screenshot3 2025-12-03 003000" src="https://github.com/user-attachments/assets/24134307-604e-4e10-b940-e762277efd05" />

From left to right Fig-1, Fig-2 and Fig-3.

• Fig-1, Fig-2 and Fig-3 shows relation between daily time and intensity , total steps and total calories respectively.

• Avg steps increases from 7:00 to 12:00 and again from 16:00 to 19:00 showing that people are most active during this time.

• Calories and average intensity also follows same trends as total steps.

### Usertype by Sleep, minutes and Totalsteps:

<img width="1064" height="297" alt="Screenshot4 2025-12-03 003000" src="https://github.com/user-attachments/assets/3be41a75-b2a6-437e-a8a4-31733e090023" />

• 58% of user have poor sleep(less than 6 hours) while only 33% have good sleep(between 6-8 hours).

• 36%(12 users) of user are very active, while 24%(8 users) are lightly active and 21%(7 users) are fairly active. Only 18%(6 users) are sedentary.  

• 21%(7 users) have more than 10000 steps (very active), 27%(9 users) have steps between 7500 and 10000 (fairly active), 27%(9 users) have steps between 5000 and 7500 (lightly active) and 24%(8 users) have less than 5000 steps (sedentary).


### Sleep pattern for different usertype:

<img width="567" height="591" alt="Screenshot5 2025-12-03 003012" src="https://github.com/user-attachments/assets/8dee5e40-6089-4905-b092-2f3d1ef59f3b" />

• Through the visuals it is clear that sedentary group has the worst sleepers and as activity increases, we see better sleep pattern. 

• Over sleepers decreases as activity level increases as more active users will spend less amount of time staying in bed.

• More data required as it seems very active user have more poor sleepers than normal sleepers but that could be because of missing data and smaller sample dataset.

### Conclusion:

1. **Daily notification on steps and posts on app:** The data shows the positive correlation between calories and steps. Thus, we can encourage users to take the recommended 7500 steps everyday by using notification when they are not meeting daily quota.

2. **Notification and sleep techniques:** Based on result most users are not getting the recommended hours of sleep i.e. 6-8 hours . Encourage users to get proper sleep by using notification and post explaining why good sleep is required.

3. **Daily use of smart device:** More than 50% users are either active or fairly active on the smart users. Thus, the device need to be more durable, water resistant and light. For other users we need to promote by they should use it more by giving more features to make it more usable in daily life.

4. **Reward system:** Most users might not get motivated by just notification so maybe there should be reward system to encourage them should they consistently reach their daily goal
