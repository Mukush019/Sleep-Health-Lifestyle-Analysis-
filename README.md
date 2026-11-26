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
- `Age` - The age of persons in years. `27 and 54.`
- `Occupation` - `Accountant`, `Doctor`, `Engineer`, `Lawyer`, `Manager`, `Nurse`, `Sales Representative`, `Salesperson`, `Scientist`, `Software Engineer`, `Teacher`
- `Sleep Duration` - Number of hours a person sleeps per day
- `Quality of Sleep` - subjective rating on a scale of 1-10
- `Physical Activity Level` - Number of minutes a person engages in physical activity per day.
- `Stress Level`- On a scale of 1-10
- `BMI Category` - Has the values `Normal`, `Normal Weight`, `Overweight`, `Obese`
- `Blood Pressure` - has the systolic and diastolic numbers
- `Heart Rate` - Number of times a resting heart beats, in beats per minute. Normal range: 60-100 
- `Daily Steps` - The number of steps a person takes per day.
- `Sleep Disorder`- The presence or absence of sleep disorder. (`None`, `Insomnia`, & `Sleep Apnea`)

## Tools

This project's data cleaning, modeling, analysis, and visualization were done in **Microsoft Power BI Desktop `Version: 2.156.951.0 64-bit (July 2026)`**.

## Data Cleaning and Modeling

The data cleaning was done in the `Power Query Editor in Microsoft Power BI`. There were no changes in the raw data. All the steps were recorded and properly labeled in the ***Applied Steps*** panel, making the process **reproducible**. A summary of the data cleaning process is in Table 1. 

|Table1: Issues Identified and Action Taken|
|----------------------------------|

|**Column**|**Issue**|**Action**|**# of Rows Affected**|
|----------|---------|----------|----------------------|
|Occupation|*Sales Representative* and *Salesperson* are similar roles under different labels|Replace *Sales Representative* with *Salesperson*|2|
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

Before building the dashboard, I explored the cleaned dataset to understand its structure, quality, and the main relationships between variables.

### Dataset Overview

- 374 records and 13 columns (15 after splitting blood pressure into systolic and diastolic).
- 185 female and 189 male participants, aged 27 to 59.
- 10 occupations after merging Sales Representative into Salesperson, 3 BMI categories, and 3 sleep disorder outcomes (None, Insomnia, Sleep Apnea).

### Data Quality Checks
Label inconsistencies and the blood pressure format were resolved during cleaning (see **Data Cleaning and Modeling**). Additional checks before analysis:

|Table 3: Summary|
|---------------------------|

| Check | Finding |
|---|---|
| Duplicates | 242 of 374 rows (65%) repeat another record's values apart from Person ID; retained and noted under Limitations |
| Range checks | All measures fall within plausible ranges; no records removed |

|Table 4: Numerical Summary|
|---------------------------|

| Measure | Min | Max | Mean | Median |
|:--------|----:|----:|-----:|-------:|
| Age (years) | 27 | 59 | 42.2 | 43 |
| Sleep duration (hrs) | 5.8 | 8.5 | 7.13 | 7.2 |
| Quality of sleep (/10) | 4 | 9 | 7.31 | 7 |
| Stress level (/10) | 3 | 8 | 5.39 | 5 |
| Physical activity (min/day) | 30 | 90 | 59.17 | 60 |
| Daily steps | 3,000 | 10,000 | 6,817 | 7,000 |
| Heart rate (bpm) | 65 | 86 | 70.2 | 70 |
| Systolic BP (mmHg) | 115 | 142 | 128.6 | 130 |
| Diastolic BP (mmHg) | 75 | 95 | 84.7 | 85 |

### Relationships Explored

Correlation with sleep quality: stress -0.90, heart rate -0.66, age +0.47, physical activity +0.19, daily steps +0.02, systolic BP -0.12, diastolic BP -0.11.

### Key Observations
- Stress is by far the strongest correlate of sleep quality and duration (-0.90 and -0.81).
- Physical activity and daily steps show weak or no linear relationship with sleep.
- 41% of participants have a sleep disorder, and the rate varies sharply by BMI category and occupation.
- Several groups are very small (Manager n=1, Scientist n=4, Software Engineer n=4), so their results should be treated cautiously.
- The ranges are narrow (stress 3 to 8, systolic 115 to 142), and many rows repeat, which suggests the data may be synthetic or heavily templated.

## Data Analysis

The analysis was carried out in Power BI using DAX measures and an interactive report of three pages: **Overview**, **Lifestyle Drivers**, and **Cardio Health**. Slicers for occupation, BMI category, and gender filter every KPI and chart, so each result can be examined for any subgroup.

### Analytical Approach

1. **Define the outcomes:** sleep duration, sleep quality, sleep disorder (Insomnia or Sleep Apnea), and blood pressure.
2. **Convert measures into shares:** thresholds turn numeric scores into proportions, such as the percentage of people sleeping under 7 hours.
3. **Compare groups:** disorder rates are compared across BMI category, age group, and occupation.
4. **Check relationships:** correlations and a scatter plot show how stress and other factors relate to sleep quality.
5. **Count people consistently:** all counts come from the fact table, because the personal information dimension holds unique profiles and not one row per person.

### Thresholds and Definitions

**Table 4: Thresholds Used in the Analysis**
|:--------|

| Concept | Definition | Source |
|:--------|:-----------|:-------|
| Sleep disorder | Sleep Apnea or Insomnia | Dataset |
| Short sleep | Sleep duration below 7 hours | Commonly recommended minimum for adults |
| Good sleep quality | Score of 7 or more (out of 10) | Analyst-defined (median score) |
| High stress | Score of 7 or more (out of 10) | Analyst-defined |
| Blood pressure categories | Normal, Elevated, Stage 1, Stage 2, Severe Hypertension | American Heart Association |

Analyst-defined thresholds are not clinical standards. They were chosen from the scale and the data distribution before looking at outcomes.

### Key Measures

**Table 5: Main DAX Measures**
|:--------|

| Measure | Purpose |
|:--------|:--------|
| `Total People` | Distinct count of people from the fact table |
| `Percentage pple with Sleep Disorder` | People with Insomnia or Sleep Apnea ÷ total people |
| `Total People (All BMI)` | Denominator that ignores the BMI filter, for BMI shares |
| `% Sleeping Below 7 Hrs` | Share of people sleeping under 7 hours |
| `% Good Sleep Quality (7+)` | Share with a quality score of 7 or more |
| `% High Stress (7+)` | Share with a stress score of 7 or more |
| `Correlation Quality vs Stress` | Pearson correlation between sleep quality and stress |
| `Blood Pressure Category` (column) | Classifies each reading from systolic and diastolic values |
| `Occupation Group` (column) | Combines occupations with fewer than 5 people into "Others" |

Because a boolean filter inside `CALCULATE` replaces a slicer on the same column, the BMI shares divide by `Total People (All BMI)`, so numerators and denominators stay consistent.

### Page 1: Overview

- **KPI cards:** average sleep duration, sleep quality, and stress, each with a share above or below its threshold, plus the share with no sleep disorder, split into Apnea and Insomnia.
- **Disorder type by BMI category:** a 100% stacked column chart showing how disorder types are distributed within each BMI group.
- **Stress vs sleep quality:** a scatter plot coloured by disorder type, with the correlation coefficient in the title.
- **Disorder rate by age group and by occupation:** bar charts of the disorder rate in each group. Occupations with fewer than 5 people are combined into "Others".
- **Key insights panel:** a short summary of the main patterns.


## Results 

## Recomendation

## Limitation 

## References

 
