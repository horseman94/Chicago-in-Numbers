# Chicago-in-Numbers
Chicago in Numbers: Exploring Crime, Education, and Inequality


### Project Overview

This project explores and analyzes key datasets from the City of Chicago to uncover relationships and patterns among socioeconomic factors, public education performance, and crime rates across various neighborhoods. By integrating these datasets, the goal is to gain a deeper understanding of how these elements interact and how they might influence each other in an urban context.
May-2025


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
- Adding headers to the tables.
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



















