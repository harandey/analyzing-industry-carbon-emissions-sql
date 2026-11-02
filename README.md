# Analyzing Industry Carbon Emissions (SQL)

This repository contains an SQL query designed to analyze industry-wise carbon footprints and active companies using the product emissions dataset.

## Query Overview

The query identifies the latest available year in the dataset, groups the data by industry, and calculates:
- The total number of distinct companies per industry group.
- The total carbon footprint (`carbon_footprint_pcf`) rounded to one decimal place, ordered in descending order to highlight the highest-emitting industries.

```sql
SELECT 
	industry_group,
	COUNT(DISTINCT company) AS num_companies,
	ROUND(SUM(carbon_footprint_pcf), 1) AS total_industry_footprint
FROM product_emissions
WHERE year = (SELECT MAX(year) FROM product_emissions)
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
