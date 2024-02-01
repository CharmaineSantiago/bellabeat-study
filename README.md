# How can Bellabeat, a Wellness Technology Company, play it smart?

![bellabeat-logo](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/74150dce-6450-492a-931c-ea476b340ad6)

# Introduction
This is the Capstone Project I completed for the Google Data Analytics Professional Certificate Course Program. I followed the Six Phases of Data Analysis Process—*Ask*, *Prepare*, *Process*, *Analyze*, *Share*, *Act*; and I used Excel, SQL Server, and Power BI in completing the entire project.  


# About the Company
Bellabeat is a high-tech manufacturer of health-focused products. With a focus on empowering women by providing knowledge about their health and habits since it was established on 2013, Bellabeat has experienced rapid growth and established itself as a tech-driven wellness company for women.
The company’s products include smart devices that can track and record activity, sleep, stress and reproductive health, and an app to which these devices can connect to. Some of these products are as follows: 
- ***Bellabeat app*** – connects to Bellabeat’s smart devices where health-related data can be tracked and recorded
- ***Leaf*** – Bellabeat’s classic wellness tracker for activity, sleep, and stress which can be worn as a bracelet, necklace, or clip
- ***Time*** – a wellness watch that tracks user’s activity, sleep, and stress
- ***Spring*** – a smart water bottle that tracks water intake


# The Data Analysis Process


## 1. Ask Phase: Getting a clear statement of the business task
Bellabeat is a successful small company with a potential to become a larger player in the global smart device market. 

1.1. Business Task: 	
- To gain insights on how consumers are currently using their non-Bellabeat smart devices and provide high-level recommendations on how these insights can inform Bellabeat’s marketing strategy

1.2. Stakeholders:
- Urška Sršen: Bellabeat’s Co-founder and Chief Creative Oﬃcer
- Sando Mur: Mathematician and Bellabeat’s Co-founder; Key member of the Bellabeat Executive team
- Bellabeat Marketing Analytics Team: A team of data analysts responsible for Bellabeat’s marketing strategy


## 2. Prepare Phase: Getting a Description of all data sources used

2.1. Data Source and Information:
- The dataset used is the FitBit Fitness Tracker Data uploaded by user Möbius on Kaggle Platform.
- Data were generated from respondents of a survey distributed via Amazon Mechanical Turk.
- 33 eligible Fitbit users consented to the submission of their personal tracker data including daily physical activity (to minute-level output), heart rate, sleep monitoring, and weight log for the period of April 12, 2016 to May 12, 2016. 
- Dataset is composed of 18 csv files, 15 of which are in long data format and the remaining three in wide format. 

2.2. Data Limitations:
- The dataset is seven years old and already outdated. 
- The 31-day time frame is insufficient for revealing actual trends in the usage of smart devices. 
- A sample size of 33 users is too small sample for the current global population of smart device users.
- Users’ demographics are lacking especially the gender information which is relevant in this case because Bellabeat’s target customers are women.
 
2.3. Data Credibility (ROCCC Method)
- Reliable – LOW 
  - Too small sample size—limited to only 33 users and only one month timeframe 
  - Users’ demographics such as age, gender, country of residence, etc. are not available 
- Original – HIGH 
  - As cited on the provenance section of Möbius’ Kaggle Notebook, the original dataset can be found on zenodo.org, a general-purpose open repository. 
  - The original dataset is published on May 31, 2016 created by Robert Furberg, Julia Brinton, Michael Keating, and Alexa Ortiz.  
- Comprehensive – MEDIUM 
  - Information included in the dataset match Bellabeat’s parameters
  - There are minor descriptions missing like the unit of distance recorded, description of hourly intensities values, and METs values. These can be clarified though through Fitabase data dictionary available online. 
- Current: LOW
  - Data is 7 years old and already outdated. 
- Cited: MEDIUM
  - Some citations from credible sites appeared during a quick online search. 

Overall, the data is not suitable to be used for producing recommendations to the business due to its limitations. However, for the purpose of a case study, the available data was still utilized and its limitations were reiterated in the recommendations section. 

2.3. Data License and Privacy
- The dataset has a Creative Commons CC0: Public Domain License which means that there is no copyright, and it is open for public to copy, modify, distribute, and be used for any purpose without asking permission.
- For data privacy, no personally identifiable information (PII) was included in the dataset and the survey respondents consented to the use of their data.


## 3. Process Phase: Documentation of data cleaning and data manipulation

3.1. Dataset used

I only investigated seven out of the 18 tables, as the remaining ones contain redundant information.  
- dailyActivity_merged
- heartrate_seconds_merged
- hourlyCalories_merged
- hourlyIntensities_merged
- hourlySteps_merged
- sleepDay_merged
- weightLogInfo_merged

3.2. Data cleaning tools and checklist

I utilized Excel and SQL Server for cleaning of small and large dataset, respectively. The list below served as my general guide in cleaning data of each file. 
- Re-name tables with proper name
- Check for accuracy and completeness of column names
- Check for accuracy and consistency of data format per column
- Check for nulls or missing values
- Check for typographical errors
- Check for extra spaces
- Check data ranges and outliers 
- Check for duplicates
- Manipulate and transform data as needed

3.3. Data cleaning findings using Excel
- File: *dailyActivity_merged*
  - Renamed file as ‘daily_activity’
  - Added "Km" to the names of columns that contain distance values, indicating that these values are in kilometers.
  - No nulls or missing values found using conditional formatting 
  - All IDs have uniform character length using LEN function
  - No duplicates found using Remove Duplicates tool under Data tab
  - Removed all rows with zero total steps as these indicates that the device was not used or worn during the day
  - Created a new column “UnaccountedMinutes” with value = 1440 – sum of the four columns containing minutes spent on each of the four intensity categories. This is to account for the remaining time of the day with no record of activity. 

- Files: *hourlyCalories_merged, hourlyIntensities_merged, hourlySteps_merged*
  - Renamed the files as ‘hourly_calories’, ‘hourly_intensities’, and ‘hourly_steps’, respectively
  - No nulls or missing values found using conditional formatting 
  - All IDs have uniform character length using LEN function
  - No duplicates found using the Remove Duplicates tool under Data tab
  - Added a new column to separate date and time values in column B using the Text to Columns tool under Data tab
  - Renamed column B as ActivityDate and formatted data to short date
  - Named column C as ActivityHour and formatted data to time

- Created a new file: *hourly_activity*
  - Created new csv file and imported the three hourly tables using the Get data tool under Data tab
  - Combined the tables—hourly_calories, hourly_intensities, and hourly_steps, using the Merge tool under Query tab
  - Re-checked data format per column
  - Saved new table as csv file 

- File: *sleepDay_merged*
  - Renamed file as ‘sleep_log’
  - Format column SleepDay values as short date
  - No nulls or missing values found using conditional formatting 
  - All IDs have uniform character length using LEN function
  - Removed three duplicate rows using Remove Duplicates tool under Data tab

- File: *weightLogInfo_merged*
  - Renamed file as ‘weight_log’
  - Format column ‘Date’ as short date
  - Removed column ‘Fat’ as only 2 rows have a value and the remaining rows are blank 
  - All IDs have uniform character length using LEN function
  - No duplicates found using the Remove Duplicates tool under Data tab

3.5. Data cleaning findings using SQL Server
- File: *heartrate_seconds_merged*
  - Created a database, ‘FitbitData’
  - Imported the file by using the right click tool > new tasks > import flat file
  - Ensured that all fields are in the right data format before uploading
  - All IDs have uniform character length using LEN function
  - Created a new table named ‘heartrate’ where date and time will be separated in two different columns 
  ```sql
  CREATE TABLE FitbitData.dbo.heartrate
  (Id bigint,
  [Date] date,
  [Time] time(7),
  [Value] int)

  INSERT INTO FitbitData.dbo.heartrate
  SELECT 
	  Id,
	  CONVERT(date,[Time]) AS [Date],
	  CONVERT(time(7),[Time]) AS [Time],
	  Value
  FROM
	  FitbitData.dbo. heartrate_seconds

  SELECT *
  FROM 
	  FitbitData.dbo.heartrate_cleaned
  ```
  ![sql-data-cleaning-heartrate](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/301e79f6-8768-4032-8bf9-23a747859b04)


## 4. Analyze Phase: Data analysis and findings

4.1. Importing files into SQL Server

Even though the dataset is small enough to work in Excel, I opted to perform the analysis using SQL. My intention is to practice and enhance various skills throughout this case study.
- Imported the following files in the created database, ‘FitbitData’, one by one by using the right click tool > new tasks > import flat file
  - daily_activity
  - hourly_activity
  - sleep_log
  - weight_log 
- Ensured that all fields are in the right data format before uploading

4.2. Users tracking each health metrics  

This section aims to determine the distinct count of users per health metric and the average number of days they tracked thru the query below. 
  ```sql
  --- daily activity
  SELECT
    COUNT(act.Id) AS users_count,
	  AVG(act.days_activity) AS avg_days_activity_tracked,
	  MIN(act.days_activity) AS min_days_activity_tracked,
	  MAX(act.days_activity) AS max_days_activity_tracked
  FROM
    (SELECT
		  DISTINCT Id,
		  COUNT(ActivityDate) OVER (PARTITION BY Id) AS days_activity
    FROM 
		  FitbitData.dbo.daily_activity
    WHERE
		  TotalSteps <> 0) AS act

  --- sleep tracking
  SELECT  
	  COUNT(sleep.Id) AS users_count,
	  AVG(sleep.days_sleep) AS avg_days_sleep_tracked,
	  MIN(sleep.days_sleep) AS min_days_sleep_tracked,
	  MAX(sleep.days_sleep) AS max_days_sleep_tracked
  FROM 
	  (SELECT
		  DISTINCT Id,
		  COUNT(SleepDay) OVER (PARTITION BY Id) AS days_sleep
  	FROM 
		  FitbitData.dbo.sleep_log) AS sleep

  --- heartrate tracking
  SELECT  
	  COUNT(heart.Id) AS users_count,
	  AVG(heart.days_heartrate) AS avg_days_heartrate_tracked,
	  MIN(heart.days_heartrate) AS min_days_heartrate_tracked,
	  MAX(heart.days_heartrate) AS max_days_heartrate_tracked
  FROM 
	  (SELECT
		  Id,
		  COUNT(DISTINCT [Date]) AS days_heartrate
	  FROM 
		  FitbitData.dbo.heartrate
	  GROUP BY
		  Id) AS heart

  --- weight tracking
  SELECT  
	  COUNT(wt.Id) AS users_count,
	  AVG(wt.days_weight) AS avg_days_weight_tracked,
	  MIN(wt.days_weight) AS min_days_weight_tracked,
	  MAX(wt.days_weight) AS max_days_weight_tracked
  FROM 
	  (SELECT
		  DISTINCT Id,
	  	COUNT(Date) OVER (PARTITION BY Id) AS days_weight
	  FROM 
		  FitbitData.dbo.weight_log) AS wt
  ```
  ![sql-analysis-health-metrics-vs-users-tracking](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/584f628f-e86d-4a8a-91e2-416773a0efe5)

4.3. Physical activity

To determine the levels of activity and its fluctuations across the hours of the day and across the days of the week, the following queries were used. 
  ```sql
  --- activity levels throughout the day
  SELECT 
	  ROUND(CAST(AVG(VeryActiveMinutes) AS float)/60, 1) AS avg_very_active_hrs,
	  ROUND(CAST(AVG(FairlyActiveMinutes) AS float)/60, 1) AS avg_fairly_active_hrs,
	  ROUND(CAST(AVG(LightlyActiveMinutes) AS float)/60, 1) AS avg_lightly_active_hrs,
	  ROUND(CAST(AVG(SedentaryMinutes) AS float)/60, 1) AS avg_sedentary_hrs,
	  24 - ROUND(CAST(AVG(VeryActiveMinutes) AS float)/60, 1) - ROUND(CAST(AVG(FairlyActiveMinutes) AS float)/60, 1) 
		- ROUND(CAST(AVG(LightlyActiveMinutes) AS float)/60, 1) - ROUND(CAST(AVG(SedentaryMinutes) AS float)/60, 1) 
		AS no_record_hrs
  FROM 
	  FitbitData.dbo.daily_activity
  WHERE TotalSteps <> 0

  --- activity levels per hour of the day
  SELECT 
	  ActivityHour,
	  AVG(StepTotal) AS avg_steps,
	  AVG(TotalIntensity) AS avg_total_intensity,
	  AVG(Calories) AS avg_calories_burned
  FROM 
	  FitbitData.dbo.hourly_activity
  GROUP BY
	  ActivityHour 
  ORDER BY
	  avg_steps DESC

  --- activity levels across the days of the week
  SELECT
	  DATENAME(WEEKDAY, ActivityDate) AS day_of_week,
	  AVG(TotalSteps) AS avg_steps,
	  ROUND(AVG(TotalDistanceKm),2) AS avg_total_distance_km,
	  ROUND(AVG(VeryActiveDistanceKm),2) AS avg_very_active_distance_km,
	  ROUND(AVG(ModeratelyActiveDistanceKm),2) AS avg_moderately_active_distance_km,
	  ROUND(AVG(LightActiveDistanceKm),2) AS avg_lightly_active_distance_km,
	  ROUND(AVG(SedentaryActiveDistanceKm),2) AS avg_sedentary_distance_km
  FROM 
	  FitbitData.dbo.daily_activity activity
  WHERE 
	  TotalSteps <> 0
  GROUP BY
	  DATENAME(WEEKDAY, ActivityDate)
  ORDER BY
	  avg_steps DESC
  ```
  ![sql-analysis-activity](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/4020e096-2fb9-4964-b2f8-1bfc8850a26b)

4.4. Sleep

Using the query below, the daily average hours of sleep and time in bed across the week were determined. 
  ```sql
  SELECT 
	  DATENAME(WEEKDAY, SleepDay) AS day_of_week,
	  ROUND(AVG(CAST(TotalMinutesAsleep AS float))/60, 1) AS avg_hrs_asleep,
	  ROUND(AVG(CAST(TotalTimeInBed AS float))/60, 1) AS avg_hrs_in_bed,
	  ROUND(AVG(CAST(TotalTimeInBed AS float))/60 - AVG(CAST(TotalMinutesAsleep AS float))/60, 1) AS diff_hrs,
	  AVG(TotalTimeInBed)-AVG(TotalMinutesAsleep) AS diff_minutes
  FROM
	  FitbitData.dbo.sleep_log
  GROUP BY
	  DATENAME(WEEKDAY, SleepDay)
  ORDER BY
	  avg_hrs_asleep DESC,
	  avg_hrs_in_bed DESC
  ```
  ![sql-analysis-sleepJPG](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/76bff594-2d06-42d1-8fc0-48a46debbd04)


## 5. Share Phase: Supporting Visualizations and Key Findings

![Viz1-health-metrics-ranked](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/aaf107e9-8f70-433f-9123-769b991f540a)

- All of the users tracked their physical activity—steps, distance, calories, activity intensity and duration, while fewer users tracked their sleep, heart rate, and weight.
- Some of the reasons may include discomfort in wearing the device during sleep, forgetting to manually record sleep and weight,  missed to turn on the heart rate tracking or maybe incorrectly wearing the device that it cannot detect heart-rate signal.


![Viz2-hours-spent-per-activity-in-a-day](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/55847c66-d9f1-44eb-8f78-637ae027f742)

- On average, users wear the device for 20 hours or 83% of the time per day. This means that the device is being casually worn almost all through the day as an accessory.
- Users spent most of their day, about 66% or almost 16 hours, in a sedentary state which involves a lot of sitting or lying down. 
- The remaining four hours of the day were consumed on varying activity levels but mostly with light active activities which may involve leisurely walk or light housework.  On average, users spent only 24 minutes being very active daily. 


![Viz3-hourly-avg-activity-and-calories](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/14706412-dbe1-4c2b-8e65-ad08a40a37b2)

- Through the day, users are most active from 5pm to 7pm, and second-most active from 12pm to 2pm.
- It can also be seen on the chart that activity levels and calories burned are positively correlated with each other. 


![Viz4-daily-avg-steps-dist-in-a-wk](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/b75911ad-96b3-4a79-a43a-e4ee36556f09)
![Viz5-sleep](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/c7fe2cbb-0fe8-4e3e-bfa2-32ff8ff8bac7)

- Across the week, users are most active on Tuesdays and Saturdays, which also when the highest number of steps and distance are reached. 
- Most of the distance travelled only any given day in a week, around 58% to 66% on average, are generated from light activities. 
- It can also be observed that the steps and distance have a positive correlation.  
- On average, users sleep within the recommended 6 to 8 hours daily and they spent 90% of their time in bed as asleep. This means that they do not likely have trouble sleeping. 
- On Sundays, users are least active, had the most hours of sleep and had a longer time, almost an hour on average, awake in bed before falling asleep.

Here is a copy of the dashboard created with Power BI containing all the previous charts. 

![dashboard](https://github.com/CharmaineSantiago/bellabeat-study/assets/158445656/4b59327c-106d-46eb-bd94-93bd849e9ec5)


## 6. Act Phase: Top High-Level Insights

To re-iterate, the key trends and findings uncovered in this study were generated from an outdated and limited dataset. I recommend that, if possible, to re-do the study using a new dataset that is updated, complete, and of sufficient sample size of users from both non-Bellabeat and Bellabeat users.  For the complete limitations of the data, return to the Prepare Phase for a review.  

***Recommendations for Bellabeat Marketing***

- Since users utilize their health tracking devices for most parts of the day and use it as an almost daily casual accessory, Bellabeat Marketing can distribute a survey to Bellabeat and non-Bellabeat users on their satisfaction level and comments regarding the devices’ visual appearance, durability, and battery life. 
- As there are fewer users who track their sleep, heart rate, and weight, Bellabeat Marketing should also account this in their survey to discover specific difficulties or concerns on this. 
- Since users are most active from 12pm to 2pm and from 6pm to 8pm, Bellabeat marketing should exploit these time slots for their advertisement and promotions. 
- To encourage the users to be more consistent in tracking their overall health and wellness, Bellabeat should consider offering a reward system to their users to boost their engagement in their goals toward healthy lifestyle.  
- Bellabeat should also organize events or group activities where not only current but also prospect Bellabeat users can interact with each other together with health experts towards building a solid community.    



  


