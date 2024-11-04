# Bellabeats: Google Data Analytics Capstone Project
This project serves as the capstone project for the Google Data Analytics Professional Certificate.

Using a public dataset, this project will use the 6 steps of the data analysis process.

![image](https://github.com/user-attachments/assets/d2b20a45-65bd-42df-99d6-3b2835239e58)

## Deliverables

1. A clear summary of the business task
2. A description of all data sources used
3. Documentation of any cleaning or manipulation of data
4. A summary of your analysis
5. Supporting visualizations and key findings
6. Your top high-level content recommendations based on your analysis



## Background
![bellabeat](https://github.com/user-attachments/assets/c7274ba6-4572-43bf-b235-2ef3c3cff23b)

Bellabeat is a high-tech company that manufactures health-focused smart products with beautifully designed technology that informs and inspires women around the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.

## Ask
**Business Task:** Analyze smart device usage data to gain insight that will guide the marketing strategy for Bellabeat.

**Key Stakeholders:** 
* Urška Sršen: Bellabeat’s co-founder and Chief Creative Officer
* Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
* Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. 

## Prepare
**Dataset**

[Fitbit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit/data) (CC0: Public Domain, dataset made available through [Mobius](https://www.kaggle.com/arashnic). This Kaggle data set contains personal fitness tracker from around thirty Fitbit users. These eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It includes information about daily activity, steps, and heart rate that can be used to explore users’ habits.


This dataset contains 18 unique CSV files:

* dailyActivity_merged
* dailyCalories_merged
* dailyIntensities_merged
* dailySteps_merged
* heartrate_seconds_merged
* hourlyCalories_merged
* hourlyIntensities_merged
* hourlySteps_merged
* minuteCaloriesNarrow_merged
* minuteCaloriesWide_merged
* minuteIntensitiesNarrow_merged
* minuteIntensitiesWide_merged
* minuteMETsNarrow_merged
* minuteSleep_merged
* minuteStepsNarrow_merged
* minuteStepsWide_merged
* sleepDay_merged
* weightLogInfo_merged

**Is It Good Data?** 
* Reliable – the dataset is reliable as it comes from Fitbit users who consented to share their data
* Original – the dataset is original as it is directly from Fitbit users
* Comprehensive – with limited users and unequal data collection, the dataset is not very comprehensive 
* Current – the dataset is not current as it is from 2016 
* Cited – not apparent

**Data Limitations**
* Limited number of users
* Lack of demographic data - unable to determine whether users are the right sample for Bellabeat
* Outdated data

## Process

**Data Cleaning**

Microsoft Excel was used for data cleaning. The main steps that were taken for cleaning were:
* Removing duplicates
* Changing data type to date
* Combining data from different time periods

## Analyze

**Tools Used:**
* Microsoft Power BI
* BigQuery - SQL

Upon reviewing and analyzing the data in each CSV file, the following files were selected for further focus:

* dailyActivity_merged
* dailySteps_merged
* hourlySteps_merged
* sleepDay_merged

The data was first analyzed in SQL and then relevant information was loaded into Power BI for further analysis and visualization.

### Device Usage

Based on analysis of total daily activity, it is possible to determine how long the device was used throughout the day. For fitness devices to be effective in collecting data for tracking, usage should be as close to 24 hours a day as possible.

```
SELECT 
  Id,
  AVG((VeryActiveMinutes + FairlyActiveMinutes + LightlyActiveMinutes + SedentaryMinutes)/60) AS TotalHours
FROM `lucky-reactor-417609.Bellabeats.dailyActivity` 
GROUP BY Id
```
![image](https://github.com/user-attachments/assets/b1ee3402-d71d-4ab0-accd-e6c278bbf51c)



### Active Days

By getting the average number of steps for each day of the week, we can see which days tend to be more active days.

```
SELECT 
  ActivityDate,
  AVG(TotalSteps) AS AverageTotalSteps
FROM `lucky-reactor-417609.Bellabeats.dailyActivity` 
GROUP BY ActivityDate
```
![image](https://github.com/user-attachments/assets/b7610a4c-bb51-4ac7-bd4b-7f01e57a5589)


### Active Hours

By getting the average number of steps for each hour of the day, we can see which hours tend to be more active throughout the day.

```
SELECT 
  ActivityHour,
  AVG(StepTotal) AS AverageStepTotal  
FROM `lucky-reactor-417609.Bellabeats.hourlySteps` 
GROUP BY ActivityHour
```
![image](https://github.com/user-attachments/assets/351b613e-46d4-439c-8e9f-a05cf0a819ed)



### Sleep

Looking at the sleep data provided, we can evaluate sleep quality and examine if there are any correlations to the day of the week. 

```
SELECT 
  SleepDay AS Date,
  AVG(TotalMinutesAsleep) AS TotalMinutesAsleep,
  AVG(TotalTimeInBed) AS TotalTimeInBed
FROM `lucky-reactor-417609.Bellabeats.sleepDay` 
GROUP BY SleepDay
```
![image](https://github.com/user-attachments/assets/4ad0d0dd-59cd-4724-80b4-433d10fbebfc)


## Share

Visualizations and results from the analysis are shared with Bellabeat along with suggestions for how to leverage their products better. A [slide deck](https://drive.google.com/file/d/15l4rBjfdViTCDcjn9dBTKrnVjtQlR7T_/view?usp=sharing) is used to share the information. 

## Act

Based on the recommendations, the Bellabeat team will be able to better market their products and improve user engagement.
