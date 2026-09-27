BigQuery Homelessness Data Analysis
Project Overview

This project analyzes public homelessness data using Google BigQuery and SQL. The analysis explores trends in overall homelessness, homeless veterans, and unaccompanied homeless youth from 2012–2018.

The goal was to clean and transform the dataset, identify meaningful trends, and determine locations with higher levels of homelessness that may require additional attention and resources.

Business Questions
How did overall homelessness change from 2012–2018?
How did veteran homelessness change over the same period?
What trends were observed among unaccompanied homeless youth under 25?
Which states and Continuums of Care (CoCs) had higher levels of homelessness?
Which locations had higher concentrations of homeless veterans and youth?
Dataset

Source: BigQuery Public Datasets — HUD Point-in-Time Homelessness

Table:

bigquery-public-data.sdoh_hud_pit_homelessness.hud_pit_by_coc

Time period: 2012–2018

The dataset contains homelessness information by Continuum of Care (CoC), including overall homelessness, veteran homelessness, and unaccompanied youth homelessness.

Data Cleaning & Transformation

I created a cleaned table in BigQuery containing the fields needed for analysis.

The original dataset was transformed by:

Selecting relevant columns
Removing unnecessary fields from the analysis table
Creating a State field using the first two characters of the CoC_Number
Organizing the data by year and location
Creating aggregated measures for overall homelessness, veterans, and youth
Example SQL transformation
SELECT
  Count_Year,
  CoC_Number,
  CoC_Name,
  LEFT(CoC_Number, 2) AS State,
  Overall_Homeless,
  Homeless_Veterans,
  Homeless_Unaccompanied_Youth_Under_25,
  Homeless_Unaccompanied_Youth_Under_18,
  Homeless_Unaccompanied_Youth_Age_18_24
FROM `bigquery-public-data.sdoh_hud_pit_homelessness.hud_pit_by_coc`;
SQL Analysis
Overall Homelessness by Year
SELECT
  Count_Year,
  SUM(Overall_Homeless) AS total_homeless
FROM `aerial-jigsaw-502321-m4.homelessness_analysis.homelessness_cleaned`
GROUP BY Count_Year
ORDER BY Count_Year;
Homeless Veterans by Year
SELECT
  Count_Year,
  SUM(Homeless_Veterans) AS total_homeless_veterans
FROM `aerial-jigsaw-502321-m4.homelessness_analysis.homelessness_cleaned`
GROUP BY Count_Year
ORDER BY Count_Year;
Homeless Youth by Year
SELECT
  Count_Year,
  SUM(Homeless_Unaccompanied_Youth_Under_25) AS total_homeless_youth
FROM `aerial-jigsaw-502321-m4.homelessness_analysis.homelessness_cleaned`
GROUP BY Count_Year
ORDER BY Count_Year;
Top Locations by Overall Homelessness
SELECT
  State,
  CoC_Name,
  SUM(Overall_Homeless) AS total_homeless
FROM `aerial-jigsaw-502321-m4.homelessness_analysis.homelessness_cleaned`
GROUP BY
  State,
  CoC_Name
ORDER BY total_homeless DESC
LIMIT 10;
Key Findings
Overall Homelessness

Overall homelessness decreased from 621,553 in 2012 to 552,830 in 2018, representing an approximately 11% decrease.

The lowest annual total occurred in 2016, with 549,928 people recorded as homeless.

Homeless Veterans

Homeless veteran counts decreased from 60,579 in 2012 to 37,878 in 2018, representing an approximately 37% decrease.

Homeless Youth

Data for unaccompanied homeless youth under 25 was available beginning in 2015 in this dataset.

Youth homelessness decreased from 36,907 in 2015 to 36,361 in 2018, an approximately 1.5% decrease overall.

However, the annual numbers fluctuated during this period, reaching 38,303 in 2017.

Visualizations

The project includes visualizations showing:
### Overall Homelessness by Year

![Overall Homelessness by Year](./overall-homelessness-by-year.png)

### Homeless Veterans by Year

![Homeless Veterans by Year](./homeless-veterans-by-year.png)

### Homeless Youth by Year

![Homeless Youth by Year](./homeless-youth-by-year.png)

### Top 10 Locations by Overall Homelessness

![Top 10 Locations by Overall Homelessness](./top-10-locations-overall-homelessness.png)

Overall Homelessness by Year
Homeless Veterans by Year
Homeless Youth by Year
Top 10 Locations by Overall Homelessness
Tools & Skills

Tools:

Google BigQuery
SQL
GitHub

Skills:

Data cleaning
Data transformation
Exploratory data analysis
SQL aggregation
Data grouping and filtering
Calculated fields
Trend analysis
Data visualization
Data storytelling
Data Limitations

The public dataset analyzed in this project contains records from 2012–2018, rather than 2010–2018.

Additionally, the Homeless_Unaccompanied_Youth_Under_25 field contains missing values for 2012–2014, so youth trend comparisons were limited to 2015–2018.

Conclusion

This analysis demonstrates how SQL and BigQuery can be used to clean, explore, and analyze a large public dataset. The project highlights changes in overall homelessness, veteran homelessness, and youth homelessness while identifying locations with higher levels of homelessness for further investigation.
