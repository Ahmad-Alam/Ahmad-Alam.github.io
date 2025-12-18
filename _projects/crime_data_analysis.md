---
layout: page
title: UK Crime Data Analysis
description: Big data analytics on UK street-level crime using Apache Spark
img: assets/img/projects/crime_types.jpg
importance: 2
category: fun
github: https://github.com/Ahmad-Alam/Crime-Data-Analysis
---

This project analyzes street-level crime data across three UK counties—Kent, Leicestershire, and Derbyshire—using Apache Spark for distributed data processing. The analysis covers all of 2022, processing hundreds of thousands of crime records to identify patterns by crime type, temporal trends, and geographic distribution.

The data processing pipeline uses PySpark to load and aggregate crime records from multiple CSV files. SQL-based analysis pipelines perform county-level aggregation, monthly trend analysis using window functions, and crime type frequency rankings. The analysis revealed that Kent experienced the highest crime volume with 200,945 incidents, followed by Leicestershire (115,179) and Derbyshire (110,805).

Key findings include the identification of violence and sexual offences as the dominant crime category across all three counties, and seasonal patterns showing crime peaks during summer months—August recorded the highest crime count in Kent with 18,365 incidents. Window functions enabled comparative analysis across regions, ranking crime types and identifying both the most and least common offenses per county.

Visualizations created with Matplotlib and Seaborn present the findings through line plots showing monthly variations, bar charts comparing crime types, and pie charts illustrating category distributions. The project demonstrates proficiency with big data tools and the ability to extract actionable insights from large-scale datasets.
