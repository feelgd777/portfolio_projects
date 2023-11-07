# Classification Models to Identify Water Pump Functionality in Tanzania


# Overview

This analysis is intended to gain an overall understanding of public and private school cafeteria violations, contrast and compare the quantity and the nature of violations in different neighborhoods and identify the areas that pose the greatest risk to public health. The analysis is conducted via **[SQL and Python](https://github.com/feelgd777/SQL_repo/blob/main/School%20cafeteria%20violations.ipynb)**, and the visualization is done with **[Tableau](https://public.tableau.com/views/Cafeteriaviolations/Dashboard3?:language=en-US&:display_count=n&:origin=viz_share_link)**.


# Data Understanding

NYC law requires a minimum of 2 inspections in a school building, each school year unannounced.
Our data is on 7,662 violations, 2,125 of which are critical. Critical violations are more likely to contribute to food-borne illnesses are considered critical. 
They are a substantial risk to the public’s health. Undersanding the sources of violations will aid in targeting problematic areas.


# Data Analysis

Main types of cafeteria records: 

* General violations 44% of all records
* Critical violations 20% 
* No violations 28%
* Administrative 5% 
* Nutrition tobacco and others 3%
  
Analysis with **SQL queries** has shown:

The count of private and public schools in our data  
The average number of violations per school  
The total count of violations  
The count of unique critical and general violations  
The count of violations by school type  
The distribution of critical and general violations by school type   
Percentage of all violations by school type  
Average number of violations per school by school type  
Top 10 categories for critical violations  
Top 10 types of critical violations  
Most common critical cafeteria violations  
A comparison of NYC boroughs based on the number of violations and average violations per school  
Average number of violations per school by borough  
Count of critical violations per neighborhood  
_____________________________________

## Where do these violation happen?

Brooklyn stands out as having the highest average violation count per school, with an average of 6 violations. This is noteworthy because, even though Brooklyn is slightly larger in terms of population compared to Queens, it has approximately 300 more registered schools as of 2023 and undergoes inspections almost twice as frequently as Queens. This could be attributed to the higher number of violations in Brooklyn, leading to more frequent inspections to ensure compliance and safety.

## Examining Population Areas

Taking a closer look at population areas (NTAs) on the map, we find that the median population for these areas is 54,000, with the highest population recorded at 132,000.
Some areas immediately draw our attention, such as Borough Park, which exhibits an average of 9.9 cafeteria violations per school. Given our focus on public health risks, we will narrow our analysis to violations related to mice and vermin, as they are the top critical violations. The darkest area on the map with regard to these violations is Greenpoint, Brooklyn, averaging 3 violations per school. However, when considering population as a factor, we identify areas with more pronounced public health risks.

Among areas with populations exceeding 100,000, Borough Park stands out with 133 mice violations across 75 schools. Astonishingly, the top 10 schools in Borough Park account for 51% of all violations in the area. These schools are primarily Jewish orthodox institutions, with only one being public, and the majority of violations originate from private schools.

## Implications
It is clear that certain areas are disproportionately affected by critical school cafeteria violations, posing higher risks to public health. There is a common belief that private schools often have more substantial budgets than public schools. It's possible that this financial flexibility allows some institutions to inadequately allocate resources for facility maintenance and general hygiene. In densely populated areas like Borough Park, there is a pressing need for increased oversight and regulations to safeguard public health. Therefore, prioritizing inspections in problematic NTAs, particularly in the case of private schools, is essential for the well-being of the public.

## Proposed Solutions
In light of our findings, we recommend the following solutions:

Implement stringent requirements for private schools to ensure compliance with health and safety standards.
Prioritize inspections in NTAs with a history of critical violations to protect public health.
Give particular attention to densely populated areas to address the heightened risk of violations and health concerns.

