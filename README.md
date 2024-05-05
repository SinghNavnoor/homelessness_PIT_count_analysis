# Homeless PIT Count Analysis
The purpose of this project is to analyze the growth of Homeless Population since 2007. Point-in-Time Count is a mandatory count of the homeless population nation wide. The goal of this project is to combine all the PIT Count datasets, analyze major trends and help create a better plan to tackle homelessness.

## Dataset
1. **Source**: 
[HUD Exchange](https://www.hudexchange.info/resource/3031/pit-and-hic-data-since-2007/)

2. **Years explored**: 
2007 - 2023

3. **Shape of the dataset**: 
- Shape of the datasets increased over the years.
- For e.g. the PIT Count 2007 dataset has 386 rows and *26 columns*, while the PIT Count 2023 has 389 rows and *646 columns*.

4. **Key Columns**

| Categorical | Numercial  | Timeframe |
|----------|----------|----------|
| CoC Name | Overall Homeless | Year |
| State_Territory | Overall Chronically Homeless |
| Count Types | Sheltered Total Homeless |
| CoC Number | Sheltered Total Chronically Homeless |

Detail the analytical methods and processes used in the project. This could include data cleaning steps, statistical methods, machine learning models, or visualization techniques.


## Methodology
The goal is to combine and clean the data without loosing a large number of rows.

#### Data Cleaning
1. Dealing with Null values in "Count Types" column.
  - "Count Types" column had 805 null values. In order to deal with them multiple strategies were used.
    - If a row had "Count Types" as null then take of column "CoC Name" and check its previous and next year's "Count Types" value. If they are the same then impute that same values in the null cell.
    - If the first condition is not true then check if either of the previous or next year value is equal to "Sheltered and Unsheltered Count", if so, then impute the null cell with this value.
    - If the second condition is also not met then check if either of the previous or next year value is equal to "Sheltered and Partial Unsheltered Count", if so, then impute the null cells with this value.
    - If the third condition is also not met then check if either of the previous or next year value is equal to "Sheltered-Only Count", if so, then impute the null cells with this value.
    
    P.S. These conditionalities took care of over half of the null values on "Count Types"
    - If null values still remained in the dataset for "Count Types" column then we imputed them with the mode of the corresponding "CoC Name" rows.
    
    P.S. This took care of over 99% of the remaining null values, leaving us with 5 null values in the column.
    - The remaining null values were imputed with the mode of the entire column.
   
#### Visualization Techniques

1. Goal: The original goal was to create a dataset for years 2017 - 2021.
2. Issue: These datasets did not give the full picture of the issue of Homelessness.

Examples:
![Overall Homeless population 2017 - 2021](https://github.com/SinghNavnoor/homelessness_PIT_count_analysis/blob/main/overall_homeless.png)

<img src="(https://github.com/SinghNavnoor/homelessness_PIT_count_analysis/blob/main/overall_homeless.png)" width="600" height="300">









