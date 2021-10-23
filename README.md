# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: Standardized Test Analysis


### Problem Statement
California has more billionaires than any other state and yet education system is ranked lowly at 41 out of 51 states([*source*](https://wallethub.com/edu/e/states-with-the-best-schools/5335)). This projects aims to analyse relationships between key demographic indicators and performance of standardized tests, and to identify areas of improvements in different counties across California.

Role: An advisor to the State of California with the task of improving education level in the various counties given limited resources.

Objective: To analyse relationships between key demographic indicators and performance of standardized tests, and to identify areas of improvements in different counties across California.

Majority of Hispanics and African-Americans in California are studying in intensely segregated schools (i.e. <10% of student population are whites). Segregation is not ideal as research has shown that it is heavily disadvantageous to the prospects of students in the minority race.([*source*](https://ssri.psu.edu/news/new-research-details-increasing-segregation-transformed-school-population))

The state of California has many schools in different counties and there are profound segregation between races in the school system. This project aims to identify counties having the lowest performance and participation rates on the SAT and ACT tests, and to identify 'at-risk' groups so that resources can be directed effectively.

With the general decline of white population, increasing segregation in school is as important to the minorities as it is to the whites. The whites will have to learn to adapt being the minority as time passes. In fact, white students no longer represent the majority of the nation's school enrollment. [source: Harming our Common Future: America's Segregated Schools 65 Years after Brown: Erica Frankenberg, Jongyeon Ee, Jennifer B. Ayscue, Gary Orfield ]

The ideal outcome is to identify at-risks counties and schools, so that more resources can be allocated to assist these groups.

### Data Dictionary

The main source of datasets used will consist of the following:

* [`act_2019_ca.csv`](./data/act_2019_ca.csv): 2019 ACT Scores in California by School
* [`sat_2019_ca.csv`](./data/sat_2019_ca.csv): 2019 SAT Scores in California by School
* [`CA_income_data_2019.csv`](./data/CA_income_data_2019.csv): 2019 income data by County
* [`acs2017_county_data.csv`](./data/acs2017_county_data.csv): 2017 demographic data by County

A brief description on the features extracted and used for analysis is shown below:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|county|object|df_analysis|The name of county|
|pct_abv_avg_score|float64|df_analysis|The percentage of grade 12 students scoring higher than the average score in ACT (>=21 points) in each county|
|participation_rate_act12|float64|df_analysis|The participation rate of ACT test amongst grade 12 enrolled students in each county|
|pct_both_bnchmk_12|float64|df_analysis|The percentage of grade 12 students scoring above the benchmark for both ERW and Math in SAT (ERW: 480, Math: 530) in each county|
|pct_both_bnchmk_11|float64|df_analysis|The percentage of grade 11 students scoring above the benchmark for both ERW and Math in SAT (ERW: 460, Math: 510) in each county|
|participation_rate_sat12|float64|df_analysis|The participation rate of SAT test amongst grade 12 enrolled students in each county|
|participation_rate_sat11|float64|df_analysis|The participation rate of SAT test amongst grade 11 enrolled students in each county|
|per_capita_income|float64|df_analysis|Income per capita of each county|
|minority|float64|df_analysis|The percentage of minority (defined as non-whites) in each county|


### Brief Summary of Analysis

In this analysis, we look into the demographics of each county and draw relations on its impacts on student performances and participation in ACT and SAT tests.

The 2 main demographic information used are mentioned in the above table:
- per_capita_income
- minority

Measure of student performances are based on the features mentioned in the above table:
- pct_abv_avg_score
- pct_both_bnchmk_12
- pct_both_bnchmk_11

Measure of student participation are based on the features mentioned in the above table:
- participation_rate_act12
- participation_rate_sat12
- participation_rate_sat11

#### Data pre-processing

**ACT and SAT Datasets (act_2019_ca.csv, sat_2019_ca.csv)**
Datasets were initially filled with multiple invalid/null values which may or may not impact on the analysis. Multiple checks were done to identify these invalid/null values and its corresponding drop rows and columns were dropped, where necessary.
There were rows with null values only in the "school_name" column. As our analysis is based on "county_name", these rows were not dropped so as to preserve the information provided in other columns.

**External demographic datasets (CA_income_data_2019.csv, acs2017_county_data.csv)**
External datasets were also used to complement the available datasets. These external datasets provide 2 important information:
- Income per capita of each county
- Minority percentage of each county
Data pre-processing was also done in the external datasets to ensure data types were appropriately converted and column names to match that of the given datasets.

These 4 datasets were then merged into 1 main dataframe ("df_analysis") based on "county_names" for subsequent analysis

#### Analysis

Exploring the data leads to a few observations:
- There were 5 counties that were consistently in the bottom 10 for performance in ACT and SAT tests. These are Colusa, Merced, Glenn, Fresno, Kings. And interestingly, all 5 counties have minority percentage more than the statewide median of 47.15%.
- There were 3 counties that were consistently in the bottom 10 for participation rates in ACT and SAT tests. These are Tuolumne, Shasta, Yuba.

For a quick overview on the potential correlations between any 2 features in the main dataframe "df_analysis", a pairplot and correlation table were produced.
Here are the general results worth mentioning:

- Higher minority percentage in a county is strongly correlated to lower performances in ACT and SAT tests.
- Higher minority percentage in a county is moderately correlated to higher participation rates in SAT tests but negligble in ACT tests.
- Higher income per capita in a county is moderately associated with higher performances in ACT and SAT tests.
- Higher income per capita in a county is moderately associated with higher participation rates in ACT and SAT tests. However, it is worth noting that correlation is more positive for SAT than for ACT.   
- Understandably so, counties with higher performances in ACT tests is strongly associated with higher performances in SAT tests.


### Conclusions and Recommendations

**Conclusions:**

From this project, we have concluded that there is a negative correlation between minority percentages and test performances. A higher minority percentage county likely means that there are racial segregation. This is also supported by research which shows high levels of racial segregation in schools leads to poorer education levels and even beyond in terms of job opportunities. ([*source*](https://ssri.psu.edu/news/new-research-details-increasing-segregation-transformed-school-population))

Furthermore, we have identified the worst performing counties that also happen to have high percentages of minority. If resources need to be allocated promptly, these are the 5 counties that require funding in terms of improving education level and racial segregation of students in schools.

**Recommendations:**

The State of California could impose a racial quota in schools, as far as possible. The racial quota should reflect the statewide percentages, so that schools have well balanced student demographics. This can potentially translate to better test performances and even better job opportunities as supported by research.

As a start, the state could look into funding the 5 counties (Colusa, Merced, Glenn, Fresno, Kings) identified as the worst performing ones which also have high levels of minority percentage. Following which, the state could look into assisting schools in Los Angeles which has the most number of schools. The main objective is to prevent racial segregation by introducing racial quota for each school. In regions where introducing a racial quota is not feasible, efforts should be introduced to promote racial integerations within schools.  

### Areas for Improvement
- Income inequality between counties/districts
- Racial proportions within each school
- Fundings within each county

### Assumptions:
- county minority percentage is used to reflect the school minority percentage (due to lack of data)
- minority percentage data was taken from 2017 data. It is assumed that there is no change between 2017 and 2019 (due to lack of data).
