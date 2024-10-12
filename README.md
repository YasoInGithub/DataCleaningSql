# DataCleaningSql
Cleaning data for analysis using SQL
# SQL Data Cleaning Project

## Project Overview

This project focuses on cleaning and preparing a dataset using SQL for further analysis. The dataset contains various data issues that need to be addressed, such as duplicates, missing values, and inconsistent formatting. The main objective is to clean the data by implementing techniques to detect and fix these issues, making it suitable for downstream analysis.

## Objectives

- **Identify and Remove Duplicates**: Use SQL's `ROW_NUMBER()` function to identify duplicate rows based on key columns and remove them, ensuring each record is unique.
- **Format Data**: Apply consistent formatting to the dataset, such as standardizing dates, trimming whitespace, and ensuring proper case for text fields.
- **Find Missing Values**: Detect missing or NULL values in important columns and populate them using known values or derived information.
- **Improve Data Quality**: By fixing data quality issues, the cleaned dataset will be more reliable and ready for analysis.

## Key Tasks

### 1. Identifying and Removing Duplicates
Using SQL's `ROW_NUMBER()` function, we can assign unique row numbers to each duplicate entry. The steps are as follows:
- Partition the data by relevant columns that define uniqueness (e.g., `id`, `name`, etc.).
- Use `ROW_NUMBER()` in conjunction with `CTE` (Common Table Expressions) to rank duplicate rows.
- Retain only the first occurrence of each duplicate, deleting the rest.

Example:
```sql
WITH RankedData AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY id, name ORDER BY date) AS row_num
    FROM your_table
)
DELETE FROM your_table
WHERE id IN (SELECT id FROM RankedData WHERE row_num > 1);
