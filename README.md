# Prepared by: Lai-Ka-Hing
# Dataset Used: Customer Purchase


<p align="center">
<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/bc764437-cbc9-4e9b-9b8c-444a75475f25" />


This repository contains a comprehensive retail customer purchase dataset capturing customer demographic profiles and multi-year product order transactions. The data integrates customer attributes—such as age, gender, country of origin, and income—with granular transactional details including product descriptions, pricing, quantities, applicable taxes, discounts, shipping costs, and fulfillment dates.

It serves as an excellent resource for exploratory data analysis (EDA), customer segmentation, purchasing behavior analysis, sales performance forecasting, revenue reporting, and evaluating buying patterns across different demographic and geographic groups.

<img width="274" height="163" alt="image" src="https://github.com/user-attachments/assets/bc764437-cbc9-4e9b-9b8c-444a75475f25" />

##5 Research Objectives Eamples
Regional Sales Performance & Geographic Market Analysis
Evaluate total revenue, transaction volume, and average order value across different geographic regions (Region) to identify high-performing markets and underperforming zones.

Impact of Discount Strategies on Net Revenue and Volume
Investigate the relationship between Discount percentages and the resulting Quantity sold versus total net Sales to determine whether discounting successfully stimulates demand or negatively impacts revenue margins.

Product Demand and Revenue Concentration Analysis
Identify which specific Product lines dominate total revenue generation and sales volume to pinpoint core revenue drivers versus low-performing inventory

Salesperson Productivity and Performance Benchmarking
Assess individual sales representatives (Salesperson) based on total sales generated, transaction frequency, and average order size to establish performance benchmarks

Temporal Sales Trends and Demand Seasonality
Examine periodic and monthly variations in sales transactions over time (Date) to detect peak purchasing windows and seasonal demand fluctuations.

## 📋 Dataset Overview

* **File Name:** `customer.csv` & 'purchase.csv'
* **Time Horizon:** Auguest 2019 – Jan 2023
* **Target Category:** Comprehensive retail
* **Key Entities:** Products, Sales Team, Regional Markets, Revenue Metrics

  Link to Jupyter Notebook in Google Colab:
  https://colab.research.google.com/drive/1zdPR2ig9qFp6Q1gPrZvky3Ac7UITW3Mv?usp=sharing
   
## 🗂️ Data Dictionary

The dataset consists of the following 10 features:

| Column Name | Data Type | Description | Example Value |
| :--- | :--- | :--- | :--- |
| **Order_ID** | String | A unique alphanumeric identifier for each transaction. | `ORD078` |
| **Date** | Date | The transaction date formatted as `YYYY-MM-DD`. | `2026-04-09` |
| **Product** | String | The name of the electronic item sold. | `Laptop`, `Mouse`, `Webcam` |
| **Category** | String | The high-level category classification. | `Electronics` |
| **Region** | String | The geographic sales territory. | `North`, `East`, `West`, `South` |
| **Salesperson** | String | The name of the account representative. | `Alice`, `Bob`, `Charlie`, `Diana`, `Ethan` |
| **Quantity** | Integer | The total units purchased in the order. | `7.0` |
| **Unit_Price** | Float | The retail price per single unit of the product. | `997.67` |
| **Discount** | Float | The promotional deduction percentage applied (0.0 to 0.15). | `0.15` (equivalent to 15%) |
| **Sales** | Float | The final calculated gross revenue earned from the order. | `6983.69` |

## 🔍 Data Quality & Cleaning Notes

If you are using this dataset for data cleaning projects, please note that it intentionally contains realistic real-world data anomalies:
* **Missing Values (NaNs):** Features like `Region`, `Salesperson`, `Unit_Price`, `Discount`, and `Sales` contain scattered missing fields (e.g., missing revenue values or unattributed regional boundaries).
* **Calculated Columns:** The `Sales` column follows the general formula:  
  \[\text{Sales} = (\text{Quantity} \times \text{Unit\_Price}) \times (1 - \text{Discount})\]
  This relationship can be exploited to programmatically restore missing metrics.
* **Empty Rows:** The raw structure contains blank structural divider rows (`,,,,,,,,,`) that should be filtered out during preprocessing.

## 🛠️ Usage Example (Python & Pandas)

Get started analyzing this dataset quickly using Python:

```python
import pandas as pd

# Load the dataset and drop completely empty structural lines
df = pd.read_csv('sales_data.csv').dropna(how='all')

# Convert date column to datetime object
df['Date'] = pd.to_datetime(df['Date'])

# Quick view of total sales revenue by product
revenue_by_product = df.groupby('Product')['Sales'].sum().sort_values(ascending=False)
print("Revenue by Product:\n", revenue_by_product)
