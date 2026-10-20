#### Prepared by: Lai-Ka-Hing
#### Dataset Used: Customer Purchase


<p align="center">
<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/bc764437-cbc9-4e9b-9b8c-444a75475f25" />


This project focuses on analyzing customer information and product purchase transactions to unlock valuable insights into buying behavior and sales performance.

## Project Overview

By combining customer demographics with transactional data, this capstone project empowers analysts to explore:

**Customer Segmentation:** Grouping customers based on profile demographics and purchasing characteristics.

**Buying Patterns & Behavior:** Understanding how different customer groups interact with products.

**Sales & Revenue Performance:** Evaluating product performance and tracking revenue trends over time.

**Customer Value Analysis:** Assessing lifetime value, spending habits, and high-value customer segments to optimize marketing and retention strategies.

**Order & Logistics Tracking:** Analyzing order fulfillment metrics, including shipping costs, delivery timelines, and product quantities ordered across different regions.

<img width="274" height="163" alt="image" src="https://github.com/user-attachments/assets/bc764437-cbc9-4e9b-9b8c-444a75475f25" />

**##5 Project Objectives**

**1.	Evaluate Product Category Performance:** Identify which product categories and specific items generate the highest sales volume and revenue contributions across different customer demographic segments.
  
**2.	Analyze Pricing and Tax Strategies:** Assess the impact of selling prices, applicable taxes, and shipping costs on overall profitability, customer demand, and order quantities.
   
**3.	Determine Seasonal and Temporal Trends:** Examine order dates and shipping timelines to uncover seasonal purchasing peaks, sales trends, and fulfillment efficiency over time.
   
**4.	Optimize Inventory and Order Management:** Review order quantities and product transaction records to improve inventory turnover, reduce carrying costs, and align stock levels with customer purchasing patterns.
   
**5.	Formulate Profitability Improvement Strategies:** Develop data-driven recommendations to enhance overall company profitability by targeting high-value customer groups and optimizing product pricing and logistics.



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
