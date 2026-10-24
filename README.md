# Sleep, Health, & Lifestyle Analytics: A Power BI Study of How Sleep Duration, Stress, Physical Activity, BMI, and Occupation Relate to Cardiovascular Health and Sleep Disorders

## Project Overview

Sleep is central to physical and mental health. Poor sleep quality and sleep disorders such as insomnia and sleep apnea are common, and they are often linked to stress, inactivity, body weight, and demanding work. Sleep is closely tied to cardiovascular health, since irregular or insufficient sleep may affect blood pressure and heart rate. This project analyzes the `Sleep, Health and Lifestyle Dataset`, which has 374 individuals aged between 27 and 59 across different occupations. It examines how lifestyle, demographic, and clinical factors relate to sleep outcomes and cardiovascular indicators.

### Objectives

#### Primary Objective
- To analyze how occupation, physical activity level, and daily steps are associated with sleep duration and sleep quality.

 #### Secondary Objective
 - To evaluate how sleep duration and sleep quality are associated with the prevalence of sleep disorders.

#### Tertiary Objective
- To examine the relationship between sleep disorders and cardiovascular/metabolic indicators such as heart rate, blood pressure, and BMI category.

### Approach

The data is cleaned and modeled in Power BI using Power Query and DAX. This includes removing inconsistencies in the BMI category column and generating fact and dimension tables. The findings will be represented in an interactive dashboard.

## Data Source

The data was downloaded from Kaggle. It is available in both CSV and XLSX formats. [Click Here](https://l1nk.dev/yt5pt4j) to download the data in XLSX format. I will be using the same format in Power BI.

The columns available in this dataset are:-

- `Person ID` - Unique identifier
- `Gender` -  Has `Male` and `Female`
- `Age` - 27 and 54
- `Occupation` - `Accountant`, `Doctor`, `Engineer`, `Lawyer`, `Manager`, `Nurse`, `Sales Representative`, `Salesperson`, `Scientist`, `Software Engineer`, `Teacher`
- `Sleep Duration` - in hours
- `Quality of Sleep` - on a scale of 1-10
- `Physical Activity Level` - in hours
- `Stress Level`- On a scale of 1-10
- `BMI Category` - Has the values `Normal`, `Normal Weight`, `Overweight`, `Obese`
- `Blood Pressure` - has the systolic and diastolic numbers
- `Heart Rate`
- `Daily Steps`
- `Sleep Disorder`- `None`, `Insomnia`, & `Sleep Apnea`

## Tools

This project's data cleaning, modeling, analysis, and visualization were done in **Microsoft Power BI Desktop `Version: 2.156.951.0 64-bit (July 2026)`**.

## Data Cleaning and Modeling

The data cleaning was done in the `Power Query Editor in Microsoft Power BI`. There were no changes in the raw data. All the steps were recorded and properly labeled in the ***Applied Steps*** panel, making the process **reproducible**. A summary of the data cleaning process is in Table 1. 

|Table1: Issues Identified and Action Taken|
|----------------------------------|

|**Column**|**Issue**|**Action**|**# of Rows Affected**|
|----------|---------|----------|----------------------|
|Occupation|*Sales Representative* and *Salesperson* are similar roles under diferent labels|Replace *Sales Representative* to *Salesperson*|2|
|BMI Category|Inconsistency in *Normal Weight* and *Normal*|Standardize to Normal Weight|195|
|Blood Pressure|Stored as text. *No aggregation or numerical analysis can be done*|Split the numbers based on `/` into `Systolic` and `Diastolic` whole numbers|374|

### Data Modeling 

This step involves creating a *star schema*. I created one fact table and three dimension tables, commonly referred to as the **Lookup Tables**. The four tables and their contents are shown in the table below, Table2. 

|Table 2: Dimension Modeling|
|---------------------------|

|**Fact Table**|**Personal Information**|**BMI Table**|**Sleep Disorder**|
|--------------|------------------------|-------------|------------------|
|Person ID|P_ID|BMI_ID|Sleep_ID|
|P_ID|Age|BMI Category|Sleep Disorder|
|BMI_ID|Age Bin|
|Sleep_ID|Gender|
|Daily Steps|Occupation|
|Diastolic|
|Systolic|
|Physical Activity Level|
|Stress Level|
|Quality of Sleep|
|Sleep Duration|
|Heart Rate|

The schema ended up as shown below. The Lookup Tables at the top and the fact table at the bottom. 

<img width="1355" height="839" alt="image" src="https://github.com/user-attachments/assets/ab1003e3-daaf-4a9e-9050-3fa14ac00c37" />

## EDA


## Data Analysis

## Results 

## Recomendation

## Limitation 

## References

 
