# Vendor Performance Analysis

## Project Overview

The **Vendor Performance Analysis** project is a data analytics solution designed to evaluate vendor performance, profitability, sales efficiency, inventory turnover, purchasing behavior, and vendor dependency.

The project integrates data from multiple sources, performs **data ingestion, cleaning, transformation, exploratory data analysis, SQL-based aggregation, statistical analysis**, and presents the final insights through an interactive **Power BI dashboard**.

The objective is to help businesses make data-driven decisions regarding **vendor selection, pricing, inventory management, procurement, and profitability optimization**.

---

## Objectives

* Analyze vendor sales and purchasing performance.
* Identify high-performing and low-performing vendors.
* Identify brands requiring promotional or pricing adjustments.
* Analyze vendor contribution to total procurement.
* Measure dependency on top vendors.
* Evaluate inventory turnover and identify slow-moving products.
* Determine capital locked in unsold inventory.
* Analyze the impact of bulk purchasing on unit prices.
* Compare profitability across different vendor groups.
* Perform statistical analysis to determine whether differences in vendor profitability are significant.
* Build an interactive Power BI dashboard for business reporting.

---

## Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **SQL**
* **SQLite**
* **Jupyter Notebook**
* **Power BI**
* **Matplotlib / Seaborn**
* **Statistical Analysis**
* **Git & GitHub**

---

## Project Structure

```text
Vendor-Performance-Analysis/
│
├── data/
│   └── *.csv
│
├── notebooks/
│   ├── Exploratory Data Analysis.ipynb
│   └── Vendor Performance Analysis.ipynb
│
├── ingestion_db.py
├── get_vendor_summary.py
│
├── vendor_sales_summary.csv
├── vendor_performance.pbix
├── Vendor Performance Report.pdf
│
└── README.md
```

---

## Project Workflow

```text
Raw CSV Data
      ↓
Data Ingestion
      ↓
SQLite Database
      ↓
Exploratory Data Analysis
      ↓
Data Cleaning
      ↓
SQL Aggregation & Joins
      ↓
Vendor Summary Table
      ↓
Feature Engineering
      ↓
Statistical Analysis
      ↓
Business Insights
      ↓
Power BI Dashboard
```

---

## 1. Data Ingestion

The `ingestion_db.py` script automatically reads CSV files from the `data/` directory and loads them into an SQLite database named:

```text
inventory.db
```

Each CSV file is stored as a corresponding database table.

The ingestion process uses:

* Pandas for reading CSV files.
* SQLAlchemy for database connectivity.
* SQLite for storing structured data.
* Python logging for monitoring the ingestion process.

---

## 2. Exploratory Data Analysis

The project performs exploratory analysis on the available database tables.

Important tables include:

* `purchases`
* `purchase_prices`
* `vendor_invoice`
* `sales`
* `begin_inventory`
* `end_inventory`

The analysis identified that inventory tables were not required for the primary vendor-performance analysis, while purchasing, sales, pricing, and freight information were essential.

EDA was used to understand:

* Data distributions
* Missing values
* Data types
* Vendor relationships
* Product pricing
* Sales performance
* Purchase behavior
* Potential outliers
* Correlations between variables

---

## 3. Data Cleaning

Several data-quality issues were identified and addressed.

### Data type correction

The `Volume` column was converted into a numerical data type.

### Missing values

Missing values were replaced with `0` where appropriate.

### Text cleaning

Leading and trailing spaces were removed from categorical columns such as:

* Vendor Name
* Description

### Feature Engineering

Several important business metrics were created:

```text
GrossProfit
ProfitMargin
StockTurnover
SalesToPurchaseRatio
```

### Formulas

**Gross Profit**

```text
Gross Profit = Total Sales Dollars - Total Purchase Dollars
```

**Profit Margin**

```text
Profit Margin = (Gross Profit / Total Sales Dollars) × 100
```

**Stock Turnover**

```text
Stock Turnover = Total Sales Quantity / Total Purchase Quantity
```

**Sales-to-Purchase Ratio**

```text
Sales-to-Purchase Ratio = Total Sales Dollars / Total Purchase Dollars
```

---

## 🗄️ 4. Vendor Summary Table

The `get_vendor_summary.py` script creates a consolidated vendor-level summary.

The summary combines:

* Purchase information
* Sales information
* Product pricing
* Freight costs
* Vendor information

SQL Common Table Expressions (CTEs) are used to separately aggregate:

* Freight
* Purchases
* Sales

These summaries are then joined to create a single analytical dataset.

The resulting table is:

```text
vendor_sales_summary
```

Creating this pre-aggregated table improves analytical performance and avoids repeatedly executing expensive joins and aggregations.

---

## 5. Key Business Questions

The project answers several important business questions.

### 1. Which brands require promotional or pricing adjustments?

Brands with **lower sales performance but higher profit margins** are identified as potential candidates for promotional campaigns, improved distribution, or pricing adjustments.

### 2. Which vendors and brands demonstrate the highest sales performance?

Vendor and brand-level sales metrics are analyzed to identify the strongest contributors to revenue.

### 3. Which vendors contribute the most to total purchase dollars?

Vendor procurement contribution is analyzed to identify the organization's most important suppliers.

### 4. How dependent is procurement on top vendors?

The analysis evaluates how much of total procurement is concentrated among the top vendors.

A high dependency on a small number of vendors can increase supply-chain risk and indicates the potential need for supplier diversification.

### 5. Does bulk purchasing reduce unit prices?

The analysis compares order sizes and purchase prices to determine whether larger purchase volumes result in lower unit costs.

The analysis found that larger orders achieved substantially lower unit prices, indicating potential cost savings through optimized bulk purchasing.

### 6. Which vendors have low inventory turnover?

Vendors with low stock turnover are identified to detect:

* Slow-moving products
* Excess inventory
* Higher inventory holding costs
* Potential obsolete stock

### 7. How much capital is locked in unsold inventory?

Unsold inventory is analyzed to determine the amount of capital tied up in products that have not generated sales.

### 8. How do profit margins differ between high- and low-performing vendors?

Profit margins are compared across vendor-performance groups using statistical analysis.

---

## Key Insights

Some of the major findings from the analysis include:

* Certain products generate negative gross profit, indicating potential pricing or cost-management issues.
* Some purchased products have zero sales, suggesting slow-moving or potentially obsolete inventory.
* Purchase and sales quantities show a very strong relationship.
* Freight costs vary significantly across vendors, highlighting potential logistics optimization opportunities.
* Larger purchase orders generally achieve lower unit prices.
* Some vendors have very low inventory turnover, indicating excess stock.
* Lower-performing vendors can maintain higher profit margins despite generating lower sales.
* Procurement is significantly concentrated among top vendors, creating potential supplier dependency risk.
* Statistical testing indicates a significant difference in profit margins between top-performing and low-performing vendor groups.

---

## Statistical Analysis

The project also performs hypothesis testing to determine whether the difference in profit margins between vendor groups is statistically significant.

### Null Hypothesis (H₀)

> There is no significant difference in the mean profit margins of top-performing and low-performing vendors.

### Alternative Hypothesis (H₁)

> The mean profit margins of top-performing and low-performing vendors are significantly different.

The statistical analysis produced a very small p-value, providing strong evidence that the difference between the two vendor groups is statistically significant.

---

## Power BI Dashboard

The processed vendor summary dataset is used to create an interactive **Power BI dashboard**.

The dashboard provides a visual overview of:

* Vendor performance
* Sales
* Purchases
* Profit
* Profit margins
* Inventory turnover
* Vendor contribution
* Freight costs
* Product performance

The Power BI report enables stakeholders to explore vendor and brand performance interactively and identify areas requiring business attention.

---

## Business Recommendations

Based on the analysis, businesses can consider:

### Vendor Management

* Maintain strong relationships with high-performing vendors.
* Evaluate low-performing vendors for improvement opportunities.
* Reduce excessive dependency on a small number of suppliers.

### Inventory Management

* Identify and reduce slow-moving inventory.
* Improve inventory planning based on sales velocity.
* Reduce capital locked in unsold products.

### Pricing Strategy

* Review products with low sales but high margins.
* Experiment with selective discounts and promotions.
* Optimize pricing based on purchase costs and market performance.

### Procurement Strategy

* Use bulk purchasing where demand and storage capacity justify it.
* Negotiate volume-based pricing with suppliers.
* Compare vendors regularly to identify cost-saving opportunities.

### Profitability Optimization

* Monitor gross profit and profit margins at vendor and brand levels.
* Investigate products generating negative or unusually low margins.
* Balance revenue growth with profitability rather than focusing only on sales volume.

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
cd Vendor-Performance-Analysis
```

### 2. Install dependencies

```bash
pip install pandas numpy sqlalchemy jupyter matplotlib seaborn
```

### 3. Add the raw CSV files

Place the required CSV files inside:

```text
data/
```

### 4. Run the data ingestion script

```bash
python ingestion_db.py
```

This creates the SQLite database and loads the raw CSV files into database tables.

### 5. Generate the vendor summary

```bash
python get_vendor_summary.py
```

This creates the consolidated:

```text
vendor_sales_summary
```

table and generates the analytical dataset.

### 6. Run the notebooks

Open Jupyter Notebook:

```bash
jupyter notebook
```

Then execute:

```text
Exploratory Data Analysis.ipynb
Vendor Performance Analysis.ipynb
```

### 7. Open the Power BI report

Open:

```text
vendor_performance.pbix
```

in Microsoft Power BI Desktop to explore the interactive dashboard.

---

## Project Deliverables

| File                                | Description                                   |
| ----------------------------------- | --------------------------------------------- |
| `ingestion_db.py`                   | Loads raw CSV data into SQLite                |
| `get_vendor_summary.py`             | Creates and cleans the vendor summary dataset |
| `Exploratory Data Analysis.ipynb`   | Database exploration and EDA                  |
| `Vendor Performance Analysis.ipynb` | Detailed vendor performance analysis          |
| `vendor_sales_summary.csv`          | Processed analytical dataset                  |
| `vendor_performance.pbix`           | Interactive Power BI dashboard                |
| `Vendor Performance Report.pdf`     | Final analytical report                       |

---

## Future Improvements

* Automate the complete ETL pipeline.
* Add real-time or scheduled data ingestion.
* Implement predictive models for vendor sales and demand forecasting.
* Develop vendor risk scoring.
* Add automated anomaly detection.
* Build a cloud-based data warehouse.
* Add automated Power BI dataset refresh.
* Develop machine-learning models for inventory optimization and sales forecasting.

---

## Author

**Sujith Royal**

Data Analytics | Python | SQL | Power BI | Data Visualization

---

## ⭐ Project Summary

**Vendor Performance Analysis is an end-to-end data analytics project that transforms raw procurement, sales, pricing, and freight data into actionable vendor-performance insights using Python, SQL, statistical analysis, and Power BI.**
