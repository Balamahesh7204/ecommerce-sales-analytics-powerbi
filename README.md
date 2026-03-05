# E-Commerce Sales & Profitability Analytics 📊

## 📌 Project Overview
This project involves an end-to-end data visualization and business intelligence solution built in Power BI. Using a comprehensive "List of Orders" dataset, the dashboard provides a deep dive into sales performance, customer purchasing behavior, and regional profitability. 

The goal of this project is to demonstrate how raw transactional data can be transformed into actionable insights that drive strategic business decisions.

## 🛠️ Tech Stack & Tools
* **Business Intelligence:** Power BI Desktop
* **Data Processing:** Power Query
* **Calculations & Logic:** DAX (Data Analysis Expressions)
* **Data Modeling:** Star Schema / Snowflake Schema design

## 📈 Key Metrics Evaluated (KPIs)
* **Total Revenue & Profit:** Overall financial performance tracking.
* **Profit Margin Analysis:** Identifying the most and least lucrative product categories.
* **Geospatial Sales Distribution:** Mapping revenue generation across different cities/regions.
* **Order Volume Trends:** Time-series analysis to identify seasonal peaks and purchasing patterns.

## 🧠 Technical Highlights
1. **Data Cleaning & Transformation:** Utilized Power Query to handle missing values, standardize data formats, and create calculated columns for deeper temporal analysis.
2. **Advanced DAX:** Formulated complex DAX queries for dynamic aggregations, time-intelligence functions (e.g., calculating moving averages and YTD sales), and conditional formatting.
3. **Data Modeling:** Established active and inactive relationships between fact and dimension tables to ensure accurate cross-filtering and seamless dashboard interactivity.

## 📂 Repository Contents
* `Retail_Profitability_Model.pbix`: The core Power BI project file containing the data model and visualizations.
* `raw_sales_data.csv`: The raw dataset used for the analysis.
* `/Screenshots`: Images of the final interactive dashboard pages.

## 💡 Key Business Insights
## 🐍 Exploratory Data Analysis (Python)
Before building the visual model in Power BI, I conducted an initial data validation and exploratory analysis using Python. This step ensures data integrity and helps identify baseline trends.

Here is a snippet of the EDA pipeline used to extract the core KPIs:

<details>
<summary><b>Click to view the Python script and output</b></summary>

### Python Script:
```python
import pandas as pd

# Load the dataset
df = pd.read_csv('data/raw_sales_data.csv') 

print("--- 1. PROFITABILITY BY CATEGORY ---")
profit_summary = df.groupby('Category')[['Sales', 'Profit']].sum()
profit_summary['Margin (%)'] = (profit_summary['Profit'] / profit_summary['Sales']) * 100
print(profit_summary.sort_values(by='Profit', ascending=False))

print("\n--- 2. CUSTOMER SEGMENTATION (AOV) ---")
segment_summary = df.groupby('Segment').agg({'Sales': 'sum', 'Order ID': 'nunique'})
segment_summary['AOV'] = segment_summary['Sales'] / segment_summary['Order ID']
print(segment_summary.sort_values(by='AOV', ascending=False))

print("\n--- 3. SEASONAL SALES TRENDS ---")
df['Order Date'] = pd.to_datetime(df['Order Date'])
df['Month'] = df['Order Date'].dt.month
monthly_sales = df.groupby('Month')['Sales'].sum()
print(monthly_sales)
