# Superstore-Sales-Data Case Study [Watch_here](https://colab.research.google.com/drive/11KWF5nJ1BlORKP1pQVjafOJ4wv26nejK?usp=drive_link)
---
Comprehensive analysis of 10,000+ transactional records from the Superstore dataset, uncovering trends in sales, profit, and customer behavior to deliver actionable business insights.

## Table of Contents
- [Project Overview](#Project-Overview)
- [Key Highlights](#Key-Highlights)
- [Key Objectives](#Key-Objectives)
- [Dataset Details](#Dataset-Details)
- [Tools & Technologies](#Tools-&Technologies)
- [Deliverables](#The-Deliverables)
- [Data Loading and Understanding](#Data-Loading-&Understanding)
- [Exploratory Data Analysis (EDA)](#Exploratory-Data-Analysis (EDA))
- [Data Analysis](#Data-Analysis)
- [Key Findings](#Key-Findings)
- [Recommendations](#The-Recommendations)
- [limitations](#The-limitations)
- [References](#The-References)

## Project Overview
---
Analyzed 10,014 sales transactions spanning 21 attributes, including customer demographics, product categories, and financial metrics (sales, profit, discount, and quantity), to identify key trends in revenue generation and to maximize profitability.

### Key Highlights:
- Advanced data cleaning techniques to ensure consistency and reliability.
- Visualized sales and profit trends to identify key growth areas.
- Customer segmentation based on sales and profitability metrics.
- Dashboard creation for presenting critical business insights effectively.

### Key Objectives
- To identify trends in sales and profitability across different regions and categories.
- To analyze the impact of discounts on profitability.
- To provide insights into customer behavior and segmentation.
- To uncover potential strategies for improving overall performance.

### Dataset Details
The dataset includes multiple sheets in an Excel file, each containing information on:

- Source: Superstore Sales dataset containing transactional data.
- Key columns: Order ID, Product ID, Sales, Profit, Category, Sub-Category, Region, Customer Segment.
- Data Period: Contains historical sales data over several years.
- Size: Approximately 10,000 rows and 21 columns.

### Tools & Technologies
- Python libraries: Pandas, NumPy, Matplotlib, Seaborn.
- Google Colab for cloud-based execution,coding and analysis.
- Excel for preliminary data examination.

### Deliverables
- Cleaned and processed dataset ready for analysis.
- Comprehensive visualizations highlighting trends and patterns.
- Detailed report summarizing key findings and actionable recommendations.
- Dashboards for presenting business insights.

### Data Loading and Understanding
- Loaded data into Pandas DataFrame and explored the structure.
- Checked data types, summary statistics, and unique values for consistency.
- Identified and documented missing values and duplicates.
- Examined key columns for potential outliers or inconsistencies.

### Exploratory Data Analysis (EDA)
- Conducted univariate, bivariate, and multivariate analysis to uncover patterns.
- Visualized sales and profit trends using line and bar charts.
- Segmented customer data to analyze performance across different regions and categories.
- Created pivot tables for advanced aggregations and percentage calculations.


### Data Analysis
- There were some interesting Code/Features I have worked with:

#### 1. Discount Analysis: 
Implemented code to correlate discount percentages with profitability metrics, utilizing scatter plots and regression models to visualize trends.

```python
# Discount Analysis: Correlation Between Discount and Profitability!
import matplotlib.pyplot as plt
import seaborn as sns

# Scatter plot: Discount vs Profit
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x='Discount', y='Profit', alpha=0.6)
plt.title('Impact of Discount on Profit')
plt.xlabel('Discount')
plt.ylabel('Profit')
plt.grid(True)
plt.show()

# Regression analysis
sns.lmplot(data=df, x='Discount', y='Profit', height=6, aspect=1.5)
plt.title('Regression: Discount vs Profit')
# Code written by Sidd!
```

#### 2. Cohort Analysis: 
Wrote Python scripts to create customer cohorts based on their first purchase date and track retention rates over time.

```python
# Cohort Analysis: Customer Retention
import pandas as pd

# Convert Order Date to datetime
df['Order Date'] = pd.to_datetime(df['Order Date'])

# Extract month and year for cohort grouping
df['OrderMonth'] = df['Order Date'].dt.to_period('M')
df['CohortMonth'] = df.groupby('Customer ID')['OrderMonth'].transform('min')

# Cohort table: Retention matrix
cohort_data = df.groupby(['CohortMonth', 'OrderMonth']).agg({'Customer ID': 'nunique'}).reset_index()
cohort_data = cohort_data.pivot(index='CohortMonth', columns='OrderMonth', values='Customer ID')

# Calculate retention rates
cohort_size = cohort_data.iloc[:, 0]
retention = cohort_data.divide(cohort_size, axis=0) * 100

# Plot heatmap
plt.figure(figsize=(12, 8))
sns.heatmap(retention, annot=True, fmt='.1f', cmap='Blues')
plt.title('Customer Retention by Cohort')
plt.xlabel('Order Month')
plt.ylabel('Cohort Month')
plt.show()

# Code written by Sidd!
```

#### 3. Profitability Heatmaps: 
Designed heatmaps using Seaborn to identify high-performing regions and categories visually.

```python
# Profitability Heatmaps: Regional and Category Performance
# Pivot table for region and category performance
heatmap_data = df.pivot_table(values='Profit', index='Region', columns='Category', aggfunc='sum')

# Heatmap visualization
plt.figure(figsize=(8, 6))
sns.heatmap(heatmap_data, annot=True, fmt='.0f', cmap='YlGnBu')
plt.title('Profitability Heatmap by Region and Category')
plt.xlabel('Category')
plt.ylabel('Region')
plt.show()
# Code written by Sidd!
```

#### 4. Shipping Mode Optimization: 
Developed logic to calculate shipping costs per mode and assess their effect on overall profitability.

```python
# Shipping Mode Optimization: Analyzing Costs and Profitability

# Calculate shipping cost per unit profit
df['ShippingCostPerProfit'] = df['Shipping Cost'] / (df['Profit'].replace(0, 1))  # Avoid division by zero

# Boxplot: Shipping mode vs Shipping cost per unit profit
plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='Ship Mode', y='ShippingCostPerProfit')
plt.title('Shipping Cost Efficiency by Mode')
plt.xlabel('Shipping Mode')
plt.ylabel('Shipping Cost per Unit Profit')
plt.grid(True)
plt.show()
# Code written by Sidd!
```

## Key Findings:
1. High discounts often resulted in negative profit margins in specific categories.
2. The "Technology" category yielded the highest profitability, while "Furniture" lagged.
3. Certain regions consistently underperformed in sales despite potential demand.
4. Customer loyalty was strongest among repeat buyers in the "Corporate" segment.

## Recommendations:
1. Reevaluate discount strategies to optimize profitability.
2. Focus marketing efforts on underperforming regions with high potential.
3. Enhance inventory management for low-performing categories.
4. Promote high-profit products in the "Technology" category through targeted campaigns.

## Limitations:
- Dataset might not include all variables influencing sales performance (e.g., external market trends).
- Data quality issues like missing values and duplicates might affect accuracy.
- Insights are based on historical data and may not predict future trends accurately.
- Lack of detailed demographic data limits customer behavior analysis depth.

## References:
- [stack_overflow](https://stackoverflow.com/)
- [Superstore_EDA Dataset provided by Coding Ninjas.](https://classroom.codingninjas.com/app/classroom/me/25145/content/894551/offering/15432443)
