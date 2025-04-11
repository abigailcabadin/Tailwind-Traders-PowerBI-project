# ![Tailwind Traders Logo](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/tailwind%20traders%20logo.jpg)

# 📊 Tailwind Traders Power BI Project

This repository showcases the **Capstone Project** for the **Microsoft Power BI Professional Certificate** on **Coursera**. The project simulates a real-world business scenario where the learner demonstrates proficiency in data preparation, modeling, analysis, and visualization using **Power BI**.

---

## 🧭 Table of Contents

- [📖 Case Study Overview](#-case-study-overview)
- [📁 Datasets](#-datasets)
- [🔍 Project Summary](#-project-summary)
- [📌 Summary of Exercises](#-summary-of-exercises)
- [📊 Power BI Reports](#-power-bi-reports)
- [🛠️ Issues Encountered & Resolutions](#️-issues-encountered--resolutions)
- [🎓 Course Skills Applied](#-course-skills-applied)
- [🚀 Outcome](#-outcome)

---

## 📖 Case Study Overview

**Tailwind Traders** is a fictional retail company that sells products across multiple countries. As a newly hired **Data Analyst**, you're tasked with delivering actionable insights using Power BI. The data spans sales transactions, customer loyalty points, product categories, returns, and supplier information.

This project is part of the **final assessment** for the **Microsoft Power BI Professional Certificate** on Coursera. It tests real-world implementation of skills such as data importation, cleaning, transformation, modeling, visualization, and storytelling using Power BI.

---

## 📁 Datasets

All raw Excel datasets used in this project are available in the repository:

- [`Tailwind Traders Sales.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Tailwind%20Traders%20Sales.xlsx)
- [`Countries.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Countries.xlsx)
- [`Purchases.xlsx`](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Purchases.xlsx) *(additional analysis not required in the original capstone project)*

---

## 🔍 Project Summary

The capstone project required the full BI lifecycle:
1. Connecting and cleaning multiple data sources (Excel files)
2. Designing a star schema and modeling data relationships
3. Creating DAX measures for advanced calculations
4. Building interactive and insightful Power BI reports
5. Enhancing usability with slicers, visuals, and dashboards

In addition to the required **Sales** and **Profit** reports, an extra **Purchases Overview** dashboard was created to provide a holistic view of Tailwind Traders' operations.

---

## 📌 Summary of Exercises

| Exercise                        | Description |
|-------------------------------|-------------|
| **Data Preparation**           | Imported and transformed data using Power Query (cleaned nulls, renamed columns, adjusted data types). |
| **Model Design**               | Built a star schema with fact and dimension tables. Linked `Sales`, `Countries`, and `Products` tables. |
| **DAX Calculations**           | Created measures using DAX: `YTD Sales`, `Median Sales`, `Profit Margin`, `Total Revenue`, `Returns`. |
| **Dashboard Creation**         | Built 3 report pages: **Sales Overview**, **Profit Overview**, and an extra **Purchases Overview** report. |
| **Interactivity**              | Implemented slicers by country and date. Used KPI cards, bar charts, pie charts, and trend lines. |

---

## 📊 Power BI Reports

### 🟦 Sales Overview
![Sales Overview](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Sales%20Overview.jpg)

- Focuses on sales quantity, loyalty points, performance by country and product
- Trend lines for median sales and product categories
- Country-based sales performance heatmap

---

### 🟨 Purchases Overview *(Bonus Report)*
![Purchases Overview](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Purchases%20overview.jpg)

- Supplier breakdown and product category purchasing
- Purchase return rates and rep feedback
- Not part of the official Coursera project — added for extended insight

---

### 🟥 Profit Overview
![Profit Overview](https://github.com/abigailcabadin/Tailwind-Traders-PowerBI-project/blob/main/Profit%20Overview.jpg)

- Key metrics: total revenue, total cost, net profit, profit margin
- Quarterly and yearly trend analysis
- Profitability by country and product category

---

## 🧮 DAX Formulas

### 📅 Calendar Table
```dax
CalendarTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2020,01,01), DATE(2025,12,31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Quarter", "Q" & FORMAT([Date], "Q")
)

### 💲 Sales in USD
Sales in USD = Sales[Sales Amount] * RELATED(ExchangeRates[ExchangeRate])
