## BASIC ANALYSIS OF THE DATASET, using SQLite

- Finding out the total number of crimes recorded.

(Analyzing the total number of crimes provides a baseline understanding of crime volume for initial assessment, benchmarking, resource allocation, public awareness, and as a foundation for deeper analysis.)

```sql
SELECT COUNT(*) FROM Chicago_Crime_Data;
```

- List community area names and numbers with per capita income less than 11000.

(This analysis helps to identify and highlight specific geographic areas characterized by lower economic status. This information can be valuable for targeted resource allocation, policy development, research and analysis, and community outreach.

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

- The community area with the highest crime prone, and the total number of crimes committed.

(It highlights the specific neighborhood with the highest concentration of criminal activity. This allows for focused law enforcement efforts, resource allocation for crime prevention.)

```sql
SELECT
    `COMMUNITY_AREA_NUMBER`,
    COUNT(*) AS Total_Crimes
FROM
    Chicago_Crime_Data
GROUP BY
    `COMMUNITY_AREA_NUMBER`
ORDER BY
    Total_Crimes DESC
LIMIT 1;
```

- Finding the name of the community area with the highest hardship index.

(It allows for focused attention and targeted interventions aimed at alleviating the complex issues contributing to hardship in that specific community.)

```sql
SELECT
    `COMMUNITY AREA NAME`
FROM
    Census_Data
WHERE
    `HARDSHIP INDEX` = (SELECT MAX(`HARDSHIP INDEX`) FROM Census_Data);
```

- Determine the Community Area Name with the most number of crimes.

(This provides a clear and understandable label for the most crime-prone area, facilitating targeted interventions, community-specific resource allocation)

```sql
SELECT
    T2.`COMMUNITY AREA NAME`
FROM
    (SELECT `COMMUNITY_AREA_NUMBER`, COUNT(*) AS CrimeCount
     FROM Chicago_Crime_Data
     GROUP BY `COMMUNITY_AREA_NUMBER`
     ORDER BY CrimeCount DESC
     LIMIT 1) AS T1
JOIN
    Census_Data AS T2 ON T1.`COMMUNITY_AREA_NUMBER` = T2.`Community Area Number`;
```



