# School Cafeteria violation analysis


# Overview

This study aims to comprehensively understand cafeteria violations in public and private schools, comparing their frequency and severity across various neighborhoods to pinpoint areas with significant public health risks. The analysis is executed using **[SQL and Python](https://github.com/feelgd777/SQL_repo/blob/main/notebooks/School%20cafeteria%20violations.ipynb)**, and the visualization is done with **[Tableau](https://public.tableau.com/views/Cafeteriaviolations/Dashboard3?:language=en-US&:display_count=n&:origin=viz_share_link)**.


# Data Understanding

The dataset contains current inspection data for cafeterias permitted in public, private, and parochial schools in NYC. It is provided by Department of Health and Mental Hygiene. The link to the dataset can be found [here](https://data.cityofnewyork.us/Health/DOHMH-School-Cafeteria-Inspections-2020-Present-/5ery-qagt).
Our dataset is on 7,662 violations, 2,125 of which are critical. The violations that are more likely to contribute to food-borne illnesses are considered critical.
They are a substantial risk to the public’s health. Understanding the sources of violations will aid in targeting problematic areas.


# Data Analysis

Main types of cafeteria records: 

* General violations 44% of all records
* Critical violations 20% 
* No violations 28%
* Administrative 5% 
* Nutrition tobacco and others 3%


<img src="./visualizations/cafeteria-violations/violations.png" width="550" height="350">
  
The analysis with **SQL queries** has provided several key insights, including:

1.  The count of private and public schools in the dataset.
2.  The average number of violations per school.
3.  The total count of violations.
4.  The count of unique critical and general violations.
5.  The count of violations by school type.
6.  The distribution of critical and general violations by school type.
7.  The percentage of all violations by school type.
8.  Average number of violations per school by school type.
9.  The top 10 categories for critical violations.
10. The top 10 types of critical violations.
11. The most common critical cafeteria violations.
12. A comparison of NYC boroughs based on the number of violations and average violations per school.
13. The average number of violations per school by borough.
14. The count of critical violations per neighborhood.

These insights provide a comprehensive understanding of the cafeteria violations dataset and help identify patterns and areas of concern related to school cafeterias in NYC.
_____________________________________

## Where do these violation happen?

To determine the average number of violations per school by borough, we ran the following SQL query:

```sql
SELECT 
    Borough,
    ROUND(CAST(COUNT(ViolationDescription) AS FLOAT) /
    COUNT(DISTINCT "Record ID"), 1) as "Average violations",
    COUNT(DISTINCT "Record ID") as "Number of Schools"
FROM schools
WHERE ViolationDescription != 'no violation'
GROUP BY Borough
ORDER BY "Average violations" DESC;
```
***SQL Query Output:***

| Borough        | Average Violations | Number of Schools |
|----------------|--------------------:|-------------------:|
| Brooklyn       | 6.0                | 635                |
| Queens         | 3.9                | 400                |
| Manhattan      | 3.7                | 312                |
| Bronx          | 3.1                | 297                |
| Staten Island  | 2.9                | 79                 |


Brooklyn stands out as having the highest average violation count per school, with an average of 6 violations. Brooklyn is slightly larger in terms of population compared to Queens, but it has over 200 more registered schools as of 2023 and undergoes inspections almost twice as frequently as Queens. This could be attributed to the higher number of violations in Brooklyn, leading to more frequent inspections to ensure compliance and safety.<br><br>

## Examining Population Areas



Taking a closer look at population areas (NTAs) on the map, we find that the median population for these areas is 54,000, with the highest population recorded at 132,000. Some areas immediately draw our attention, such as Borough Park, which exhibits an average of 9.9 cafeteria violations per school. Given our focus on public health risks, we will narrow our analysis to violations related to mice and vermin, as they are the top critical violations.

### SQL Analysis:
To identify the neighborhoods with the highest concentration of mice and vermin violations, we used the following SQL query:

```sql
SELECT 
    "NTA Name", 
    COUNT(*) AS "Critical violations"
FROM schools
WHERE ViolationLabel = 'Mice, rats, vermin'
GROUP BY "NTA Name"
ORDER BY "Critical violations" DESC
LIMIT 10;
```

**SQL Query Output**

| NTA Name                | Critical Violations |
|-------------------------|---------------------:|
| Borough Park            | 133                 |
| Williamsburg            | 50                  |
| Bedford                 | 30                  |
| Canarsie                | 23                  |
| Rugby-Remsen Village    | 22                  |
| Flatbush                | 21                  |
| East New York           | 20                  |
| Sunset Park West        | 19                  |
| Crown Heights South     | 19                  |
| Bushwick South          | 19                  |

*This table displays the top 10 neighborhoods with the highest number of mice and vermin violations.*

Among areas with populations exceeding 100,000, Borough Park stands out with 133 mice violations across 75 schools. Astonishingly, the top 10 schools in Borough Park account for 51% of all violations in the area. These schools are primarily Jewish orthodox institutions, with only one being public, and the majority of violations originate from private schools.

### Tableau Visualization:
The Tableau visualization below further illustrates these findings, highlighting Borough Park as a significant public health concern. The darkest area on the map, Greenpoint, Brooklyn, averages 3 violations per school, but when considering population as a factor, Borough Park's risk is more pronounced. Astonishingly, the top 10 schools in Borough Park account for 51% of all violations in the area. These schools are primarily Jewish orthodox institutions, with only one being public, and the majority of violations originate from private schools.

<img src="./visualizations/cafeteria-violations/Tableau-screen.png" width="900" height="500">

## Implications
It is clear that certain areas are disproportionately affected by critical school cafeteria violations, posing higher risks to public health. There is a common belief that private schools often have more substantial budgets than public schools. It's possible that this financial flexibility allows some institutions to inadequately allocate resources for facility maintenance and general hygiene. In densely populated areas like Borough Park, there is a pressing need for increased oversight and regulations to safeguard public health. Therefore, prioritizing inspections in problematic NTAs, particularly in the case of private schools, is essential for the well-being of the public.

# Proposed Solutions
In light of our findings, we recommend the following solutions:

Implement stringent requirements for private schools to ensure compliance with health and safety standards.
Prioritize inspections in NTAs with a history of critical violations to protect public health.
Give particular attention to densely populated areas to address the heightened risk of violations and health concerns.

