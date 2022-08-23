

# Case Study: How Can a Wellness Technology Company Play It Smart?

## Background

Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the global smart device market. Urška Sršen, co-founder and Chief Creative Officer of Bellabeat, believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. 

Urška Sršen and Sando Mur founded Bellabeat, a high-tech company that manufactures health-focused smart products. Sršen used her background as an artist to develop beautifully designed technology that informs and inspires women around the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.

Sršen knows that an analysis of Bellabeat’s available consumer data would reveal more opportunities for growth. She has asked the marketing analytics team to focus on a Bellabeat product and analyze smart device usage data in order to gain insight into how people are already using their smart devices. Then, using this information, she would like high-level recommendations for how these trends can inform Bellabeat marketing strategy.

You have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The insights you discover will then help guide marketing strategy for the company. You will present your analysis to the Bellabeat executive team along with your high-level recommendations for Bellabeat’s marketing strategy.

----

## Defining Business Task 

### Business Task

- **How consumers are using their smart devices.** 

### Deliverables

A report with the following deliverables:
1. A clear summary of the business task
2. A description of all data sources used
3. Documentation of any cleaning or manipulation of data
4. A summary of analysis
5. Supporting visualizations and key findings
6. Top high-level content recommendations based on your analysis

### Stakeholders

#### Primary

- ***Urška Sršen:*** Bellabeat’s co-founder and Chief Creative Officer
- ***Sando Mur:*** Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team

#### Secondary

- ***Bellabeat marketing analytics team:*** A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’’s mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.

## Data-set Integrity Check and Cleaning Preparation

### Tools Used 

- DB Browser for SQLite (SQL) - For exploring, processing and cleaning of data (Some of the files contained rows more than Excel can handle)
- Tableau - Analysis and visualization

### Data & Source Integrity

#### Reliability

Data used for this project is from a fitness tracking device under brand Fitbit open/public data which can be found in this [link](https://www.kaggle.com/datasets/arashnic/fitbit). The data is about fitness data from 30 individuals wearing Fitbit fitness tracker. Since there is no information regarding participants' age, sex and profession, accuracy and unbiased stand can not be vetted. 

#### Originality

Data set contains 30 user fitness tracking data down to the minute. This data was collected by Amazon Mechanical Turk between 03.12.2016 - 05.12.2016. This data has been preprocessed and uploaded by Kaggle user [Mobius](https://www.kaggle.com/arashnic). Data set is under Creative Commons license which claims no copyright of the data and allows copy, modification and performing work, even for commercial purposes, all without asking permission. Details of the license can be found [here](https://creativecommons.org/publicdomain/zero/1.0/)

Since data has been collected from third party and was preprocessed as well, originality can not be vetted as well.

#### Comprehensiveness

30 eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. However, there are some discrepancies in the data set:

- There is no information about the age, sex, height and profession of the personnel providing fitness logs. This makes identifying pattern of activity of individual  
- dailyActivities_merged.csv contains distance data but there is no information regarding distance measuring unit.
- There are inconsistencies in logged data. Not all participants have full 30 days of data. Moreover, Since this data spreads for both May and April months, there are participants with 31 days of data. This makes the time-frame for data analysis inconsistent. 
- Some of the data contains 1440 mins of Sedentary minutes which is equivalent to  hour. This indicates not wearing the tracker throughout the day.
- There are no information regarding what intensity is and how to measure and unit of intensity in the hourlyIntensities_merged.csv

#### Data Colletion Period

This data was collected by Amazon Mechanical Turk between 03.12.2016 - 05.12.2016. This indicates that data is quite outdated. This decreases usability of the data.

#### Citation

Digital Object Identifier (DOI) is 10.5281/zenodo.53894 which resolves to [this](https://doi.org/10.5281/zenodo.53894)

### Data-set Observations

- The Fitbit data set contains 18 files containing different tracking data. These are:
  1. dailyActivity_merged.csv
  2. dailyCalories_merged.csv
  3. dailyIntensities_merged.csv
  4. dailySteps_merged.csv
  5. heartrate_seconds_merged.csv
  6. hourlyCalories_merged.csv
  7. hourlyIntensities_merged.csv
  8. hourlySteps_merged.csv
  9. minuteCaloriesNarrow_merged.csv
  10. minuteCaloriesWide_merged.csv
  11. minuteIntensitiesNarrow_merged.csv
  12. minuteIntensitiesWide_merged.csv
  13. minuteMETsNarrow_merged.csv
  14. minuteSleep_merged.csv
  15. minuteStepsNarrow_merged.csv
  16. minuteStepsWide_merged.csv
  17. sleepDay_merged.csv
  18. weightLogInfo_merged.csv
- dailyActivity_merged.csv contains all the column data from dailyCalories.csv, dailyIntensities.csv, dailySteps.csv.
- Some of the data are in both long and wide format. These are calorie, heart rate and steps data.
- heartrate_seconds_merged.csv contains heart rate of an individual for 24 hrs at 15 seconds interval.
- ***Summary of logged data:***

| Logged Data |    Second-wise     |    Minute-wise     |     Hour-wise      |      Day-wise      |
| :---------: | :----------------: | :----------------: | :----------------: | :----------------: |
|  Calories   |        :x:         | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
|  Intensity  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Heart rate  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
|    Sleep    |        :x:         |        :x:         |        :x:         | :heavy_check_mark: |
|   Weight    |        :x:         |        :x:         |        :x:         |     Inadequate     |

## Cleaning and Processing Data

The data set has been marked as pre-processed. There is less chance of blanks or dirty data. However, in order to clean obtained data following cleaning activities have been performed:
- The date format of the daily and hourly data logs were modified with excel to 'YYYY-MM-DD HH:MM:SS' format for ease of future calculations.

- Checking for blank values - none found

  ```sql
  -- This has been repeated for all of the field of the table
  SELECT id
  FROM dailyActivity_merged_date_mod
  WHERE id is NULL
  ```

- Checking for negative values using following query - none found

  ```sql 
  SELECT
  	min(TotalDistance), max(TotalDistance),
  	min(TotalSteps), max(TotalSteps),
  	min(LoggedActivitiesDistance), max(LoggedActivitiesDistance),
  	min(SedentaryActiveDistance), max(SedentaryActiveDistance),
  	min(SedentaryMinutes), max(SedentaryMinutes),
  	min(Calories), max(Calories)
  FROM
  	dailyActivity_merged_date_mod
  ```

- Checking for full day sedentary activities in the dailyActivities_merged.csv as this can provide overview of each of the individuals daily activity patterns. 

  ```sql
  SELECT
  	id,
  	SedentaryMinutes, 
  	count() AS 'Sedentary Days (=> 1440 mins)'
  FROM
  	dailyActivity_merged_date_mod
  WHERE
  	SedentaryMinutes >= 1440
  GROUP BY
  	id, SedentaryMinutes
  ```
  **Result:**

  | ID         | Sedentary Days (=> 1440 mins) |
  | :--------- | :---------------------------: |
  | 1503960366 |               1               |
  | 1844505072 |               9               |
  | 1927972279 |              13               |
  | 4020332650 |              14               |
  | 4057192912 |               1               |
  | 4319703577 |               1               |
  | 4388161847 |               1               |
  | 4702921684 |               1               |
  | 5577150313 |               2               |
  | 6117666160 |               5               |
  | 6290855005 |               4               |
  | 6775888955 |               9               |
  | 7007744171 |               1               |
  | 7086361926 |               1               |
  | 8253242879 |               1               |
  | 8583815059 |               6               |
  | 8792009665 |               9               |

  

- Since this data spreads for both May and April months, there are participants with 31 days of data. There are inconsistencies in logged data as not all participants have full 30 days of data as well As a result, weekly cycle has been considered and 4 weeks (28 days) have been taken in consideration for time-frame of analysis since most of the participants' logged data can be taken into analysis.

  ```sql
  SELECT
  	id, count() as days_logged
  FROM
  	dailyActivity_merged_date_mod
  GROUP BY
  	id
  ORDER BY
  	days_logged
  ```

  !s[./screenshots/days_logged.jpg]

  

  ```sql
  -- Extracting 28 days of user acitvity data with no full day sedentary.
  SELECT
  	d_active.Id,
  	d_active.ActivityDate,
  	d_active.TotalSteps,
  	d_active.TotalDistance,
  	d_active.TrackerDistance,
  	d_active.LoggedActivitiesDistance,
  	d_active.VeryActiveDistance,
  	d_active.ModeratelyActiveDistance,
  	d_active.LightActiveDistance,
  	d_active.SedentaryActiveDistance,
  	d_active.VeryActiveMinutes,
  	d_active.FairlyActiveMinutes,
  	d_active.LightlyActiveMinutes,
  	d_active.SedentaryMinutes,
  	d_active.Calories
  FROM
  	dailyActivity_merged as d_active
  INNER JOIN 
  	(SELECT Id
  	FROM dailyActivity_merged
  	GROUP BY Id
  	HAVING count(Id) >= 28) as d4w
  ON 
  	d_active.Id = d4w.Id
  WHERE
  	d_active.SedentaryMinutes < 1440
  ```

  

  This query resulted 760 rows of user activity data which was analyzed in Tableau.

- Along with the above mentioned extracted table, sleepDay_merged.csv has been used for analysis.

## Analyzing and Visualizing Data

As per available data, following correlations have been analyzed and visualized:

### Avg. Steps Taken Weekly

In the first analysis average steps taken by the participants weekly has been observed and found that Sunday being the lowest, 6991 steps, Tuesday and Saturday shares higher number which is above 8000 and other days are roughly around 7500 steps.

<img src='./visualizations/Average Steps Taken Through Weekdays_2color.png' width=1024>

Moreover, breakdown of each participants' average step counts throughout the weekdays have been plotted for better understanding of the movement pattern of the participants.

<img src='./visualizations/Avg Steps Taken by Participants on Weekdays.png' width=668>

#### Speculation

Participants are not consistent with maintaining their movement. On Sunday (holiday) participants tend to be more sedentary than the other days of the week. Moreover, it has been observed that most of the participants do not meet the 10,000 steps recommendation by CDC (Centers for Disease Control and Prevention) [1].

### Participants' Pattern of Being Sedentary

The below mentioned table portrays each participants'  sedentary days. This helps to observe which participant is more careful and serious about wearing the fitness tracker and measure sedentary and activity minutes.

Moreover, average sedentary minutes by participants have been plotted in color mapped table in the following picture and it can be observed that almost half of the participants seem to have higher sedentary minutes.

<img src='./visualizations/Avg Sedentary Minutes of Participants.png' width= 920>

#### Speculation

1. Half of the participants spend most of the day without any significant movement or exercise which has been marked in Red colored shades.
2. Some of the participants have high number of sedentary days, indicating fitness tracker not being worn. Similar incident might have happened for the dark red shades of the color mapped table above which might be the result of tracker not being worn for some part of the day.

### Time Spent in Different Activity Categories

Time spent in different activity types has been visualized by weekdays. This shows that most of the time spent by the participants is in the lightly active category averaging 192.7 minutes. Although average very active time (21.8 minutes) is slightly higher than the fairly active time (13.6 minutes) spent throughout the weekdays, these values are far behind the lightly active minutes.

<img src='./visualizations/Active Time.png' width=986>

#### Speculation

Light activity includes regular daily activities such as walking slowly, sitting and using computer, light standing work i.e. cooking, washing dishes etc., fishing sitting, playing instruments etc[2]. Above visualization means that most of the participants are not very active and conscious about being active and keeping healthy lifestyle.

### Calories Burnt During Active Time

Average calories burnt during active time on weekdays has been measured and visualized. Here, summation of lightly active, moderately active and very active time has been considered as "Total Active Minutes". Average of Total Active Minutes and Average of Calories Burnt throughout the weekdays have been plotted.

<img src='./visualizations/Avg Calories Burnt During Active Time.png' width=737>

Moreover, the average calories burnt by the individual participants has been analyzed and it has been observed that half of the participants have calories burnt below 2000 mark.

<img src='./visualizations/Avg Calories Burnt by Participants.png' width=737>

#### Speculation

Calorie burning requirement differs according to age, body weight, sex and calorie intake. These information are missing in this data set. Only weight information is available but for only 8 IDs and none of these weight logs represent any changes overtime. However, despite all of these missing information, as per general guideline women typically burn about 2000 calories per day and men burn about 2500 calories per day[3]. As per this guideline, the calories burnt throughout the weekdays are within this range.

### Sleeping Durations of Participants

Average sleep duration of the participants throughout the weekdays have been measured and visualized in order to get information about average sleeping hours and sleeping patterns of participants.

<img src='./visualizations/Sleep Durations.png' width=484>

#### Speculation

Although there were not age information of the participants, it is recommended that an adult (18-60 years) gets 7 hours and more sleep everyday [4]. In contrast to this information, most of the participants sleep duration is less than 7 hours on weekdays apart from Sunday, which is holiday.

## Summary

Although the data set lacked reliability and comprehensiveness due to lack of proper data collection time-line; participants age, gender, sex and profession the data set yielded some usage pattern of the Fitbit fitness tracker users. Since healthy life-style gets down to participants' calorie usage and resting pattern, the activity time, steps taken, calories burnt, sedentary habits and sleep durations have been analyzed and visualized.  Firstly, in case of activity it has been observed that most of the participants do not meet the 10,000 steps requirement by CDC. Moreover, half of the participants spend most of the day without any significant movement. However, the calorie burning requirement meets the desired value (men 2500 cal, women: 2000 cal) for half of the participants. This might be indicative of light exercise being done by the participants. On the other hand, considering sedentary condition, 1/3 of the participants have very high value of sedentary minutes. Some of the sedentary values might be indicative of tracker not being worn all the time throughout the day. On account of sleep, average sleeping duration is below 8 hour mark even Sunday being the highest  with 7.1 hours.

## Conclusion and Recommendation

As per Bellabeat stakeholder recommendation, Fitbit user open data has been analyzed to identify patterns of fitness device usage. Although the data set lacked some information, as per analysis following recommendations can be provided:

1. There has been high number of sedentary minutes observed in the data set. Potential cause of it might be not wearing the fitness tracker for long time in a day. The tracker needs to have feature to identify when it's on the users body or not. Otherwise this can produce wrong information about the user.
2. Users need to be notified about the lacking activity periodically. Users can be emailed most appropriately show as notification on the cellphone screen. In addition, calorie intake tracking can be introduced and thus curated activity plan can be suggested by the application.

## References

1. Lifestyle Coach Facilitation Guide: Post-Core: https://www.cdc.gov/diabetes/prevention/pdf/postcurriculum_session8.pdf
2. Examples of Moderate and Vigorous Physical Activity: https://www.hsph.harvard.edu/obesity-prevention-source/moderate-and-vigorous-physical-activity/
3. How Many Calories Should You Burn Daily: https://www.nike.com/a/how-many-calories-should-you-burn-daily
4. How Much Sleep Do I Need?: https://www.cdc.gov/sleep/about_sleep/how_much_sleep.html
