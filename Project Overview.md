# Chicago-in-Numbers
Chicago in Numbers: Exploring Crime, Education, and Inequality.


### Project Overview

This project explores and analyzes key datasets from the City of Chicago to uncover relationships and patterns among socioeconomic factors, public education performance, and crime rates across various neighborhoods. By integrating these datasets, the goal is to gain a deeper understanding of how these elements interact and how they might influence each other in an urban context.



### Data Sources

1. Socioeconomic Indicators in Chicago
Years Covered: 2008–2012
This dataset contains six key socioeconomic indicators of public health significance, along with a calculated “hardship index,” for each of Chicago’s 77 community areas.

[Link](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2)

2. Chicago Public Schools – Progress Report Cards (2011–2012)
School Year: 2011–2012
Performance data for all public schools in Chicago used to create CPS School Report Cards. This includes test scores, attendance rates, and other key performance indicators.

[Link](https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t)

3. Chicago Crime Data (2001–Present)
Years Covered: 2001 to Present (excluding the most recent 7 days)
This dataset reflects all reported crime incidents in the City of Chicago, excluding murders (which are recorded per victim).

[Whole.Dataset.Link](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2) , [Subset.Link](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoCrimeData.csv?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01)

### Tools
- SQLite

### Data Cleaning/Preparation

- Data loading and inspection.
- Making sure columns have headers.
- Changing the names of tables to shorter ones.

### Basic Data Analysis

- Finding out the total number of crimes recorded.

(Analyzing the total number of crimes provides a baseline understanding of crime volume for initial assessment, benchmarking, resource allocation, public awareness, and as a foundation for deeper analysis.)

```sql
SELECT COUNT(*) FROM Chicago_Crime_Data;
```

- List community area names and numbers with per capita income less than 11000.

(This analysis helps to identify and highlight specific geographic areas characterized by lower economic status. This information can be valuable for targeted resource allocation, policy development, research and analysis, community outreach.

```sql
SELECT
    `COMMUNITY AREA NAME`,
    `Community Area Number`
FROM
    Census_Data
WHERE
    `Per Capita Income` < 11000;
```

- Listing all case numbers for crimes involving minors and kidnapping crimes involving a child.

(This inquiry allows for deeper investigation into the circumstances surrounding crimes involving minors and children, as well as Pattern recognition.)

```sql
SELECT
    ID,
    CASE_NUMBER,
    DESCRIPTION
FROM
    Chicago_Crime_Data
WHERE
    DESCRIPTION LIKE '%MINOR%' OR DESCRIPTION LIKE '%CHILD%';
```
  
- Listing each kind of crime and its count that were recorded at schools.

(This helps to quickly identify the most and least frequent types of criminal activity occurring in school environments. This allows for a focused understanding of the specific safety and security challenges schools face, enabling targeted interventions and resource allocation to address the most prevalent issues.)

```sql 
    SELECT
    DESCRIPTION,
    COUNT(*) AS Crime_Count
FROM
    Chicago_Crime_Data
WHERE
    LOCATION_DESCRIPTION LIKE '%SCHOOL%'
GROUP BY
    DESCRIPTION;
```
- Listing the types of schools along with the average safety score for each type.

(This can quickly highlight whether one type of school, on average, reports higher or lower safety levels, potentially informing resource allocation, policy adjustments, or further investigation into the factors contributing to these differences.)

```sql
SELECT
    `Elementary, Middle, or High School`,
    AVG(`Safety Score`) AS Average_Safety_Score
FROM
    Chicago_Public_Schools
GROUP BY
    `Elementary, Middle, or High School`;
```

- Listing the 5 community areas with the highest percentage of households below the poverty line.

(To pinpoint the neighborhoods facing the most significant economic hardship. This allows for targeted interventions, resource allocation, and policy focus to address poverty and support vulnerable communities in those specific areas.)

```sql
SELECT
    `COMMUNITY AREA NAME`,
    `PERCENT HOUSEHOLDS BELOW POVERTY`
FROM
    Census_Data
ORDER BY
    `PERCENT HOUSEHOLDS BELOW POVERTY` DESC
LIMIT 5;
```








