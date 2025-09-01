# Analyzing EV and Hybrid car adoption in Washington State (2025) Data Analytics Project

## Project Overview

### Introduction
This project analyzes **electric and hybrid vehicle adoption trends in Washington State (2025)** using **SQL** for data cleaning and **Tableau** for interactive visualization.  

The goal of the project is to answer these key **business questions**:
- Which counties have the most electric cars?
- What are the most popular car brands and models?
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

## Source & License
- **Publisher:** data.wa.gov — Washington State Open Data Program
- **Maintainer:** Washington State Department of Licensing
- **License:** Open Data Commons Open Database License (ODbL) v1.0
- **Attribution:**  
  Contains information from the State of Washington Open Data Program, licensed under the Open Data Commons Open Database License (ODbL).

---

## Data Processing
Before even touching the data, I verified that the dataset contained all the necessary data required to answer all the key business questions.
Shortly after doing this, I began on data transformations. The first modification was to the Clean Alternative Fuel Vehicle column. Originally, it contained long descriptive strings like:

***"Eligibility unknown as battery range has not been researched"***

I standardized these into concise values such as:

***"unknown"***

Why? Because one of the key responsibilities of a data analyst is to consider the audience. Visualizations should communicate insights quickly and clearly. Long strings of text can confuse or overwhelm viewers, making it harder to interpret the message at a glance. By cleaning and standardizing this column, I ensured that the visuals are easy to understand, drastically improving the audience's experience.
