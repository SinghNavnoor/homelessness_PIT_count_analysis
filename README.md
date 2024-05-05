# Homeless PIT Count Analysis
Homelessness has become an increasingly large issue in American society. This project aims to analyze the growth of the homeless population from 2007 to 2023, using Point-in-Time (PIT) Count datasets provided by the U.S. Department of Housing and Urban Development (HUD). The PIT Count is a federally mandated survey that enumerates individuals and families experiencing homelessness across the country. The primary goals of this project are to merge these datasets, explore major trends in homelessness and the provision of shelters, and identify potential strategies to mitigate this pressing issue.

## Dataset
1. **Source**: 
[HUD Exchange](https://www.hudexchange.info/resource/3031/pit-and-hic-data-since-2007/)

2. **Years explored**: 
2007 - 2023

3. **Shape of the dataset**: 
- As the years have passed, the number of variables in the dataset has steadily increased.
- For example, the PIT Count 2007 dataset contains 386 rows and *26 columns*, while the PIT Count 2023 has 389 rows and *646 columns*.
- This increase in variables has had a net positive impact. It allows for more detailed analysis based on the population's age, race, gender and other demographic factors. This enhanced granularity aids in undersanding the diverse needs of the homeless population and developing targetted interventions.

4. **Key Columns**

| Categorical | Numercial  | Timeframe |
|----------|----------|----------|
| CoC Name | Overall Homeless | Year |
| State_Territory | Overall Chronically Homeless |
| Count Types | Sheltered Total Homeless |
| CoC Number | Sheltered Total Chronically Homeless |

5. **Explaing the columns**
- CoC Name: CoC stands for Continuum of Care. A CoC is a regional or local planning body that is responsible for coordinating the funding of services provided to homeless families and individuals. A CoC can contain a region of a city, an entire city, a group of cities or even counties.
- CoC Number: It is a unique number assigned to every CoC.
- Count Types: This column refers to the different methods each CoC used to count the homeless population. Such as Sheltered & Unsheltered Count or Sheltered Only Count.

## Methodology
Goal: Merge and clean the datasets without loosing a significant number of rows.

#### Data Cleaning
1. **Dealing with Null values in "Count Types" column:**
   
  - Imputing null values in this variables is crucial for properly analyzing any relationships between the types of counts conducted and the outcomes.
  - The variable initially had 805 null values.
  - Employed a hierarchical imputation system based on the data's contextuality:

    a. If "Count Types" was null, first referenced the "CoC Name" to check the "Count Types" value in the previous and following years. If they matched, that value was imputed.

    b. If the values varied then the following values would be given preference in specified order:
      1. "Sheltered and Unsheltered Count"
      2. "Sheltered and Partial Unsheltered Count"
      3. "Sheltered-Only Count"

   
      - These steps resolved over half of the null values in "Count Types."
    
    c. If null values still remained, they were imputed using the mode of the "Count Types" for rows under the same "CoC Name."

      - This method addressed over 99% of the remaining nulls, leaving only five.
    
    d. The last few null values were impute with the mode of the entire "Count Types" column.

This systematic approach ensured data integrity and improved the robustness of our subsequent analyses.

   
#### Visualization Techniques

Goal: The original goal was to create a dataset for years 2017 - 2021.

Issue: These datasets did not give the full picture of the crisis of homelessness as they showed a decrease in the population in 2021.

Examples:
<div>
  <img src="overall_homeless.png" width="500" height="400">
  <img src="chronically_homeless_17_21.png" width="500" height="400">
</div>

**Solution**: Combined all 17 datasets spanning from 2007 to 2023, resulting in a more clear picture of the cirsis.

<div>
  <img src="overall_homeless_07_23.png" width="500" height="400">
  <img src="chronically_homeless_07_23.png" width="500" height="400">
</div>

## Explanatory Analysis
- Uilized Tableau to created visualization showing:
  - The U.S. map with homeless population per state from 2007 to 2023.
  - The population growth of Overall Homeless from 2007 to 2023 and how many were sheltered.
  - The population growth of Chronically Homeless from 2011 to 2023 and how many were sheltered.

Link to the Visualization: 
[PIT Count Analysis 2007 - 2023](https://public.tableau.com/app/profile/navnoor.kahlon/viz/PITCountAnalysis2007-2023/Story3)

## Specialized Datasets
The combined dataset provided an extensive look into the homeless population count. However, the dataset is also plagued with thousands of null values. These null values exist mainly because that specific column was not present in that year's dataset. The Unified dataset is divided into sections. For example, the first column of a section would be "Overall Homeless" then the following 15 columns would explore different aspect of it such as the Overall Homeless - age group, race, gender and ethnicity. This finding brought the need to create specialized datasets that can be used for analysis and future model building.

### General Column Dataset
- This dataset consists of the columns common among all the 17 datasets. Additionally, these common columns can also be considered the general categories under which further variables were created in the following years.
- Shape of the dataset: (6516, 28)
- The number of null values dropped drastically in this dataset with "Unsheltered Chronically Homeless Individuals" column having the most at 39.
- This dataset was used for explanatory analysis on tableau.

### Chronically Homeless Dataset
- This dataset specilizes in the Chronically Homeless population.
- As found in the exploratory analysis of the unified dataset the count for the Chronicaly Homeless population didn't start until 2011, so the dataset contains rows from year 2011 onwards.
- Shape of the dataset: (4986, 21)
- The highest number of null values were in column "Unsheltered Chronically Homeless People in Families" at 44.
- This dataset was used for explanatory analysis on tableau. 

## SQL Exploration
### 1. Highest recorded homeless population
  <img src="4_result_highest_population.png" width="500" height="300">

### 2. Highest & lowest percentage of sheltered homeless population
#### By State
<div>
  <img src="5_highest_sheltered_result.png" width="400" height="300">
  <img src="5_lowest_sheltered_result.png" width="400" height="300">
</div>

#### By Year
<div>
  <img src="5_highest_sheltered_result_by_year.png" width="400" height="300">
  <img src="5_lowest_sheltered_result_by_year.png" width="400" height="300">
</div>

### Highest ratio of Chronically Homeless population to Overall Homeless population
#### By State - CoC - Year
<div>
<img src="2_result_s.png" width="300" height="200">
<img src="2_result_coc.png" width="300" height="200">
<img src="2_result_year.png" width="300" height="200">
</div>


## Further ideas to explore
1. Retrieve the amount of money spent by every state, every year on homelessness. Analyze if spending more resulted in the decline of homelessness.
2. Create a Time Series model, per state, that can predict the following year's homeless population.









