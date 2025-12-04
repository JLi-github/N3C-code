Environment & Versions

SQL: Compatible with MySQL 8.0 and PostgreSQL 13+, ensuring cross-database functionality for data extraction and manipulation.

R: Tested on R 4.2.2 to guarantee reproducibility of analysis scripts.

R Packages: Utilizes dplyr, tidyverse, and data.table for efficient data wrangling, transformation, and summarization.

Data Structure: OMOP Common Data Model (CDM), which standardizes clinical data to facilitate consistent analysis across multiple datasets.

SQL Query Overview

This SQL script is designed to process vaccination data in combination with associated health conditions. It performs a series of steps to prepare a clean, analysis-ready dataset and to identify relevant events for downstream analyses. The workflow includes:

Extract Outcome History:

Retrieves historical records of health conditions prior to vaccination.

Helps identify individuals with pre-existing conditions, which can affect risk analyses.

Filter Cohort:

Excludes individuals who already had the outcomes of interest.

Computes key dates such as vaccination date, study entry, and observation windows to define the analysis cohort.

Define Final Dataset:

Calculates risk periods relative to vaccination.

Incorporates death_date to censor follow-up appropriately, ensuring accurate person-time calculations.

Identify First Event Time:

Determines the earliest occurrence of a condition within the observation window.

Critical for distinguishing incident events from pre-existing conditions.

Classify Events:

Labels events according to their timing relative to vaccination:

pre_ref_event: Occurred before the reference date.

risk_event: Occurred during the defined risk period post-vaccination.

post_ref_event: Occurred after the risk period.

This classification enables clear separation of baseline versus exposure-related outcomes for analysis.

Additional Notes:

The script is designed for modular use: each step can be run independently to inspect intermediate results.

The workflow ensures data integrity by handling missing values, overlapping dates, and censoring events due to death or study exit.

While written for MySQL/PostgreSQL, the logic is adaptable to other SQL-compatible platforms with minimal changes.
