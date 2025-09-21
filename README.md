# Analyzing EV and Hybrid car adoption in Washington State (2025) Data Analytics Project

## Project Overview

### Introduction
This project analyzes **electric and hybrid vehicle adoption trends in Washington State (2025)** using **SQL** for data cleaning and **Tableau** for interactive visualization.  

The goal of the project is to answer these key **business questions**:
- What are the top 10 counties with the most electric cars?
- What are the top 5 most popular car brands in the top 10 counties?
- Are fully electric cars (BEVs) more common than plug-in hybrids (PHEVs)?
- How has EV adoption changed by model year?
- Which cars have the best electric range?
- How does price relate to range?
- Which electric utilities serve the most EVs?

### Tools
The main tools that will be used for this project are **SQL(Postgres)** for the data cleaning and analysis, and **Tableau(Tableau Public)** for the data visualization and dashboard creation

### Personal Goals
- Improve my data cleaning and analytical skills
- Improve my dashboard creation skills with Tableau
- Improve my ability to use SQL to obtain data insights
- Improve my data storytelling ability
  
### Dataset Information
The dataset used for this project was obtained from Kaggle's public datasets.
The dataset contains the following columns
- VIN
- County
- City
- State
- Postal code
- Model year
- Make
- Model
- Electric Vehicle Type
- Clean Alternative Fuel Vehicle (CAFV) Eligibility
  
If you wish to visit the dataset yourself, use the following link!
https://www.kaggle.com/datasets/samanfatima7/2025-electric-and-hybrid-cars-in-washington-usa

### Term Key
**Electric vehicle type column**
- Battery Electric Vehicle = BEV
- Plug-in Hybrid Electric Vehicle = PHEV
  
**Clean alternative fuel vehicle eligibility column**
- Eligibility unknown as battery range has not been researched = unknown
- Clean Alternative Fuel Vehicle Eligible = eligible
- Not eligible due to low battery range = not eligible

### Source & License
- **Publisher:** data.wa.gov — Washington State Open Data Program
- **Maintainer:** Washington State Department of Licensing
- **License:** Open Data Commons Open Database License (ODbL) v1.0
- **Attribution:**  
  Contains information from the State of Washington Open Data Program, licensed under the Open Data Commons Open Database License (ODbL).

---

## Data Processing
**Firstly**, before even touching the data, I verified that the dataset contained all the necessary data required to answer all the key business questions.
Shortly after doing this, I began on data transformations. The first modification was to the Clean Alternative Fuel Vehicle column. Originally, it contained long descriptive strings like:

***"Eligibility unknown as battery range has not been researched"***

I standardized these into concise values such as:

***"unknown"***

Why? Because one of the key responsibilities of a data analyst is to consider the audience. Visualizations should communicate insights quickly and clearly. Long strings of text can confuse or overwhelm viewers, making it harder to interpret the message at a glance. By cleaning and standardizing this column, I ensured that the visuals are easy to understand, drastically improving the audience's experience.

**Secondly**, I carried out an additional transformation, this time targeting the electric_vehicle_type_v1 column. The objective was twofold: first, to simplify the original values into more digestible categories for clearer visualizations, and second, to consolidate all transformations into a single, streamlined table to facilitate analysis.

Originally, this column contained long strings like:

***"Battery Electric Vehicle (BEV)"***

I standardized these into concise labels such as:

***"BEV"***

To achieve this, I took a slightly different approach than before. Instead of creating multiple intermediate tables for each transformation, I referenced the original query as a subquery within the new statement. This allowed me to apply both transformations on electric_vehicle_type_v1 and clean_alternative_fuel_vehicle_eligibility in one go, resulting in a new table called ev_adoption_port_project_processed.

This greatly aids my analysis as consolidating transformations into a single query reduces complexity and improves performance. It also ensures that all cleaned data is readily available for analysis and visualization, without the need to track multiple transformation steps across different tables.

### With that, we finish with our data processing and begin our analysis!

---
## Data Analysis
### Question 1: “What are the top 10 counties with the most electric cars?”
**To begin**, I started by validating that the dataset contained the necessary fields to answer our first question!
“What are the top 10 counties with the most electric cars?”
This ensured that the analysis would be accurate and based on complete data.

I proceeded by writing an initial query to count vehicles by county using COUNT(*) with a GROUP BY clause for county. However, I quickly noticed this approach contained a major mistake as VIN values can appear multiple times due to duplicate registrations or updates, which would instantly ruin the accuracy of the query.

To correct this, I updated the query to use COUNT(DISTINCT vin). This guarantees that each unique vehicle is counted only once, providing a truly accurate measure of electric vehicle distribution by county.
Finally, I added an ORDER BY clause to sort the results in descending order and applied LIMIT 10 to return only the top 10 counties. This helps me streamline the visualization.
With that, the first question has been answered!

The final step for this question is **visualization**, which, for this particular question, is straightforward, as the best way to demonstrate the top 10 countries is a bar chart. Through the visualization of the data, the dominance of King became clear.
King possesses more EVs than any other county. Even when taking into account its closest competitor, Snohomish King still possesses 5,319 move EVs.

**Based on this insight**, I would recommend an organization trying to break into the Washington state region to try one of two things
- **Break into the existing King market** If an EV seller is attempting to have success from the start, the best place to begin is King, as its population has a taste for EVs already.
- **Build your own new market** Based on the success of EVs in King, it can be inferred that other neighboring counties could develop a taste for EVs of their own. If immediate gains are not the priority, it is worth considering trying to build your own market of EVs in another county.

### Question 2: "What are the top 5 most popular car brands within the top 10 counties?"
To answer this question, I created a query to see the number of EVs owned for each brand in each county. The query was straightforward, as I wanted to do all the filtering and manipulating in Tableau to further develop my skills on that end.
Although the query did go through multiple iterations as I was unsure of how to handle the COUNT function. The version I ended up with is COUNT(DISTINCT vin) as it accurately counts unique EVs while  avoiding duplicates. It also groups by both make and county, giving a clear breakdown of EV adoption by brand in each location.

After completing the visualization through a mixture of filters and sets, I was able to draw multiple conclusions that can be used in a variety of business scenarios. The main pattern I noticed was that the distribution of EV ownership became more skewed
in Tesla's favor as you went down the list.

**Based on this insight** If an EV manufacturer is trying to break into the Washington market, they must be careful about which county they strike, as the smaller counties clearly favor Teslas more than any other EV brand. 
My recommendation would be to start with the larger markets like King or Pierce before expanding as their markets clearly show more brand diversity. 

### Question 3: "Are fully electric cars (BEVs) more common than plug-in hybrids (PHEVs)?"
To answer this question, I created a query to isolate the EV type for each distinct vehicle using its VIN. The goal was to determine whether fully electric cars (BEVs) are more common than plug-in hybrids (PHEVs). I used PostgreSQL’s DISTINCT ON function, which allowed me to extract only one row per VIN, ensuring that each vehicle was counted once, even if it appeared multiple times in the dataset.

Afterward I completed the visualization in the form of a pie chart, which showed that BEVs are preferred 25% more than PHEVs.

**Based on this insight** If an EV manufacturer is trying to break into the Washington market, they should prioritize making BEVs, as the market has a preference for that type of vehicle.

