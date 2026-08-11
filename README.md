![Tailwind Traders Logo](https://raw.githubusercontent.com/abigailcabadin/Tailwind-Traders-PowerBI-project/main/tailwind%20traders%20logo.jpg)

# Tailwind Traders Power BI Project

This repository showcases the **Capstone Project** for the **Microsoft Power BI Professional Certificate** on **Coursera**. The project simulates a real-world business scenario where the learner demonstrates proficiency in data preparation, modeling, analysis, and visualization using **Power BI**.

---

## Table of Contents

- [Case Study Overview](#-case-study-overview)
- [Datasets](#-datasets)
- [Project Summary](#-project-summary)
- [Summary of Exercises](#-summary-of-exercises)
- [Power BI Reports](#-power-bi-reports)
- [Issues Encountered & Resolutions](#️-issues-encountered--resolutions)
- [Course Skills Applied](#-course-skills-applied)
- [Outcome](#-outcome)

---

## Case Study Overview

**Tailwind Traders** is a fictional retail company that sells products across multiple countries. As a newly hired **Data Analyst**, you're tasked with delivering actionable insights using Power BI. The data spans sales transactions, customer loyalty points, product categories, returns, and supplier information.

This project is part of the **final assessment** for the **Microsoft Power BI Professional Certificate** on Coursera. It tests real-world implementation of skills such as data importation, cleaning, transformation, modeling, visualization, and storytelling using Power BI.

---

## Datasets

All raw Excel datasets used in this project are available in the repository:

- [`Tailwind Traders Sales.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Tailwind%20Traders%20Sales.xlsx)
- [`Countries.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Countries.xlsx)
- [`Purchases.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Purchases.xlsx) *(additional analysis not required in the original capstone project)*

---

## Project Summary

The capstone project required the full BI lifecycle:
1. Connecting and cleaning multiple data sources (Excel files)
2. Designing a star schema and modeling data relationships
3. Creating DAX measures for advanced calculations
4. Building interactive and insightful Power BI reports
5. Enhancing usability with slicers, visuals, and dashboards

In addition to the required **Sales** and **Profit** reports, an extra **Purchases Overview** dashboard was created to provide a holistic view of Tailwind Traders' operations.

---

## Summary of Exercises

| Exercise                        | Description |
|-------------------------------|-------------|
| **Data Preparation**           | Imported and transformed data using Power Query (cleaned nulls, renamed columns, adjusted data types). |
| **Model Design**               | Built a star schema with fact and dimension tables. Linked `Sales`, `Countries`, and `Products` tables. |
| **DAX Calculations**           | Created measures using DAX: `YTD Sales`, `Median Sales`, `Profit Margin`, `Total Revenue`, `Returns`. |
| **Dashboard Creation**         | Built 3 report pages: **Sales Overview**, **Profit Overview**, and an extra **Purchases Overview** report. |
| **Interactivity**              | Implemented slicers by country and date. Used KPI cards, bar charts, pie charts, and trend lines. |

---

## Power BI Reports

### Sales Overview

![Sales Overview](https://raw.githubusercontent.com/abigailcabadin/Tailwind-Traders-PowerBI-project/main/Sales%20Overview.jpg)

- Focuses on sales quantity, loyalty points, performance by country and product
- Trend lines for median sales and product categories
- Country-based median sales

---

### Purchases Overview *(Bonus Report)*

![Purchases Overview](https://raw.githubusercontent.com/abigailcabadin/Tailwind-Traders-PowerBI-project/main/Purchases%20overview.jpg)

- Supplier breakdown and product category purchasing
- Purchase return rates and rep feedback
- Not part of the official Coursera project — added for extended insight

---

### Profit Overview

![Profit Overview](https://raw.githubusercontent.com/abigailcabadin/Tailwind-Traders-PowerBI-project/main/Profit%20Overview.jpg)

- Key metrics: total revenue, total cost, net profit, profit margin
- Quarterly and yearly trend analysis
- Profitability by country and product category

---

## DAX Formulas

### Calendar Table
```dax
CalendarTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2020,01,01), DATE(2025,12,31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Quarter", "Q" & FORMAT([Date], "Q")
)
```

### Sales in USD
```dax
Sales in USD = Sales[Sales Amount] * RELATED(ExchangeRates[ExchangeRate])
```

### Profit USD (Calculated Column)
```dax
Profit USD = Sales[Net Revenue USD] - Sales[Total Cost USD]
```

### Yearly Profit Margin
``` dax
Yearly Profit Margin = 
DIVIDE(
    SUM(Sales[Profit USD]),
    SUM(Sales[Gross Revenue USD])
)
```

### Quarterly Profit
```dax
Quarterly Profit = 
CALCULATE(
    SUM(Sales[Profit USD]),
    DATESQTD(CalendarTable[Date])
)
```

### Median Sales
```dax
Median Sales = MEDIAN(Sales[Sales Quantity])
```

### YTD Profit
```dax
YTD Profit = 
CALCULATE(
    SUM(Sales[Profit USD]),
    DATESYTD(CalendarTable[Date])
)
```

---

## Issues Encountered & Resolutions

### 1. Python Script Import Error (Missing Module)

**Issue**:  
While importing exchange rate data using a Python script in Power BI, I encountered the following error:
``` makefile
Details: "ADO.NET: Python script error.
Traceback (most recent call last):
  File "...PythonScriptWrapper.PY", line 2, in <module>
    import os, pandas, matplotlib
ModuleNotFoundError: No module named 'pandas'"
```

**Resolution**:
- Installed the missing pandas library by running:
  
```bash
  pip install pandas
```

- Restarted Power BI Desktop to reload Python dependencies.
- Configured Power BI to use the correct Python environment under File > Options and settings > Options > Python scripting.

---

### 2. 🧾 Incorrect Field Names and Table Reference in DAX
**Issue**: Dax formulas were returning errors due to:
- A space in the column name (Exchange Rate instead of ExchangeRate)
-Incorrect table name from the python script output (df was not properly referenced)

**Resolution**:
- Renamed the column to ExchangeRate (removed the space).

---

### 3. 🔧 Data Model Adjustment

**Issue**: The new `Sales in USD` table needed a calculated column for `Profit USD`, and it was crucial to maintain correct relationships to allow for time-intelligence functions (e.g., YTD).

**Resolution**:
- Created a new calculated column using DAX for `Profit USD`.
- Reviewed and validated relationships across all relevant tables to ensure time-aware calculations worked as expected.

---

### 3. Chart Formatting Challenges

**Issue**: Dashboard visuals, especially slicers and axis labels, were not responsive or well-aligned initially, leading to a cluttered user experience.

**Resolution**:
- Fine-tuned the slicer behavior and adjusted axis scaling and sorting.
- Aligned visuals for consistent layout and improved readability.

---

## Course Skills Applied

- Data extraction and transformation with **Power Query**
- Designing dimensional data models (star schema)
- DAX functions for custom metrics and KPIs
- Time intelligence using `DATESYTD`, `DATESQTD`, `YEAR`, `QUARTER`
- Interactive dashboard creation with slicers, cards, pie/bar/line charts
- Usability and storytelling through visual design

---

## Outcome

This project demonstrates end-to-end proficiency with Power BI. From cleaning and modeling to storytelling with interactive dashboards, this capstone proves readiness to take on real-world analytics roles.

---
> Built with ❤️ by [Abigail Cabadin](https://github.com/abigailcabadin)
