# Wazzuf Job Postings Analytics Handout

## Executive Summary
The goal of this project is to create a one-page Power BI dashboard to visualize hiring trends from Wazzuf job postings. The dashboard leverages a dataset of 25,115 job postings with 13 fields, sourced from `workfile.csv`. The project involves data preparation using Power Query, data modeling with a star schema in Power BI, designing five interactive visuals, and deploying the dashboard to Power BI Service with scheduled daily refreshes.

## Project Overview

### Objective
Develop an interactive Power BI dashboard with five visuals to analyze Wazzuf job posting trends, including filters for dynamic exploration, and publish it to the web.

### Scope
- **Data Preparation**: Clean and transform data using Power Query in Excel.
- **Data Modeling**: Import the cleaned Excel file into Power BI and create a star schema.
- **Dashboard Design**: Build the dashboard using Power BI Desktop with five interactive visuals.
- **Deployment**: Publish the dashboard to Power BI Service and configure scheduled refreshes.

## Data Preparation

### Source
- **File**: `workfile.csv`
- **Records**: 25,115
- **Fields**: 13 (e.g., job_title_full, job_title_additional_info, work_mode, location, years_of_experience)

### Cleaning Steps
1. **Work Mode Classification**:
   - Extracted work mode ("Remote", "Hybrid", "Onsite") from `job_title_full` and `job_title_additional_info` columns.
   - Merged these columns and applied an `IF` statement to create a new `work_mode` column:
     - Keywords in `job_title_full` or `job_title_additional_info` determined the mode (e.g., "remote" for Remote).
     - Records without keywords defaulted to "Onsite".
   - Uppercased and trimmed values for consistency.

2. **Location Cleaning**:
   - Duplicated the main table in Power Query to focus on location data.
   - Removed unnecessary columns (e.g., `job_posting_id`).
   - Split the `location` column by delimiter (",") into parts (e.g., city, state, country).
   - Added custom columns for `city`, `state`, and `country` using `IF` statements to standardize values.
   - Merged the cleaned location table with the main table.

3. **Applicant Classification**:
   - Created a new column to categorize the number of applicants (e.g., Low, Medium, High) based on thresholds.
   - Loaded the cleaned data into Excel for import into Power BI.

## Data Modeling & Measures

### Data Import
- Imported the cleaned Excel file into Power BI via Power Query connection.

### Star Schema
- Created a star schema with the following structure:
  - **Fact Table**: `fact_job_postings` (primary table with job posting details).
  - **Dimension Tables**:
    - `work_mode` (Remote, Hybrid, Onsite)
    - `industry` (e.g., Internet & Services)
    - `location` (city, state, country)
    - `job_titles` (job roles)
    - `skills` (linked via a bridge table for job skills).
  - Established primary keys for each table and relationships with `fact_job_postings`.

### Measures
- **Average Experience Years**:
  ```dax
  Average Experience Years = AVERAGE(fact_job_postings[Years_of_Experience])
  ```
  - Calculates the average years of experience required across job postings.

## Dashboard Design

The "Geo-distribution on Wazzuf Job Website" dashboard provides insights into Wazzuf job postings with the following features:

- **Key Metrics**:
  - Total Jobs Posted: 25,115
  - Average Experience Required: ~4 years
- **Visuals**:
  1. **Bar Chart**: Top job categories (e.g., Internet & Services as the leading category).
  2. **Map**: Geographic distribution of job postings across the US.
  3. **Pie Chart**: Breakdown of job types (e.g., Full-Time, Part-Time, Contract).
  4. **Line Graph**: Job posting trends from 2017 to 2021 (peak in 2019).
  5. **Key Stats Card**: Displays total jobs and average experience.
- **Filters**:
  - Work Setup: Remote, Onsite, Hybrid
  - Job Levels: Entry, Mid, Senior
  - Time: Months and Years
- **Interactivity**: Filters allow users to drill down into specific trends.

## Deployment & Sharing
- Published the dashboard to Power BI Service.
- Configured a gateway to the source file (`workfile.csv`) for scheduled daily refreshes.
- **Next Refresh**: Configured for daily updates (e.g., 5/30/2025 at 00:00 AM).
- **Web Link**: [Click here to view the dashboard](https://app.powerbi.com/view?r=eyJrIjoiZDUyYmI4YjMtMDRkOS00NWE4LTg4OTgtODFkYTJkZGY0ZWNmIiwidCI6IjEzMmI2Y2RkLTM0YzktNDUxZS1hNjNjLWQwMGQ1ZmEyZjZhNyIsImMiOjl9)

## Usage
This dashboard is ideal for HR professionals, job seekers, and market analysts to explore Wazzuf job trends interactively. The clean layout and filters make it easy to focus on specific job categories, locations, or time periods.
