# Indian-Districts-Population-Data
📌 Project Overview

This project presents a comprehensive Population Analytics Dashboard built using Power BI, with data sourced originally from a CSV file, migrated to MySQL, and then imported into Power BI via a direct database connection.
The dashboard visualizes population distribution, district counts, district-wise ranking, and sex-ratio insights across Indian states.

📂 Data Pipeline
1️⃣ CSV Source

Original dataset: population_raw.csv

Columns include: State, District, Population, SexRatio, Year

2️⃣ Migration to MySQL

The CSV file was imported into a MySQL database for structured storage and easier querying.

Database: population_db
Table: district_data

Example SQL setup:

CREATE DATABASE population_db;
USE population_db;

CREATE TABLE district_data (
  State VARCHAR(100),
  District VARCHAR(100),
  Population BIGINT,
  SexRatio FLOAT,
  Year INT
);

LOAD DATA INFILE '/path/to/population_raw.csv'
INTO TABLE district_data
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 LINES;

3️⃣ Power BI Connection

Data was imported into Power BI using the MySQL Database Connector:

Home → Get Data → MySQL Database

Loaded the table district_data

Applied transformations via Power Query:

Data type corrections

Removing nulls

Cleaning district names

Ensuring numeric formats

📊 Dashboard Visuals (Based on the Photo Provided)
1. Count of Districts by State (Pie Chart)

Shows how many districts exist in each state

Uttar Pradesh dominates (69 districts ~ highest share)

Helps compare state administrative sizes

2. Sum of Population by State (Bar Chart + Line Overlay)

Displays total population per state

Uses ascending/descending sorting

Line chart overlays trend patterns

Uttar Pradesh, Maharashtra, Bihar show highest values

3. Sum of Population by District (Bar Chart)

District-wise population comparison

Highest-population districts appear on the left

Automatically sorted using ranking logic

4. Sum of Sex Ratio by District (Donut Chart)

Visualizes sex-ratio distribution

Each ring segment represents a district

Percentage breakdown gives quick demographic insight

5. District Selection Panel (Slicer)

Allows interactive filtering

Users can select any district to update all visuals

Works dynamically with rank & totals

🏆 Ranking Logic (Used in District Population Ranking)
DAX Measures
Total Population = SUM(district_data[Population])

District Rank =
RANKX(
    ALL(district_data[District]),
    CALCULATE([Total Population]),
    ,
    DESC,
    DENSE
)

District Rank (Dynamic) =
RANKX(
    ALLSELECTED(district_data[District]),
    CALCULATE([Total Population]),
    ,
    DESC,
    DENSE
)


Descending order → highest population = Rank 1

Dynamic behavior when the user applies slicers

📌 Dashboard Purpose

This dashboard helps users:

✔ Compare population across states and districts
✔ Identify highest and lowest-population districts
✔ Analyze sex-ratio distribution
✔ Explore district counts per state
✔ Understand demographic patterns visually
✔ Use dynamic slicers to explore specific states or districts

🚀 Deployment Notes

To publish in Power BI Service, configure a Gateway for MySQL

Use scheduled refresh if database updates

Credentials stored securely via data gateway



📄 Summary

This population analytics dashboard provides a clean and interactive visual exploration of India’s demographic distribution. The combination of MySQL backend storage and Power BI visualization makes it scalable, dynamic, and ideal for BI reporting.


Show what the dashboard looks like.---  ![Dashboard Preview]()
