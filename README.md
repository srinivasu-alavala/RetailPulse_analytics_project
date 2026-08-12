# RetailPulse — Retail Transaction Analytics & Business Intelligence

> An end-to-end Data Analytics project transforming 1M+ real-world retail transactions into actionable business insights using Python and Power BI.

---

## 1. Project Overview

**RetailPulse** is an end-to-end Data Analyst portfolio project designed to transform raw retail transaction data into business-ready insights.

The project covers:

- Data profiling and quality assessment
- Data cleaning and transformation
- Exploratory Data Analysis (EDA)
- Customer RFM segmentation
- Customer churn/inactivity analysis
- Product and demand analysis
- 30-day demand forecasting
- Inventory planning
- Interactive Power BI reporting

### Business Objective

The project aims to help retail stakeholders understand:

- Sales and revenue performance
- Customer value and retention risk
- Product demand
- Future demand
- Inventory replenishment requirements

---

# 2. Business Problem

Retail transaction data often contains missing values, duplicates, cancellations, negative quantities, and pricing anomalies.

The business needs a reliable analytical solution to answer:

1. How is revenue changing over time?
2. Which countries and products generate the most value?
3. Which customers are most valuable?
4. Which customers require retention attention?
5. Which products show strong demand?
6. What demand can be expected over the next 30 days?
7. How can demand forecasts support inventory planning?

---

# 3. Dataset

## Online Retail II

The project uses the **Online Retail II** dataset from the **UCI Machine Learning Repository**.

### Dataset Overview

- **Total Records:** 1,067,371
- **Columns:** 9
- **Period:** December 2009 – December 2011
- **Unique Customers:** 5,942
- **Unique Invoices:** 53,628
- **Unique Products:** 5,305
- **Countries:** 43

### Dataset Sources

**Official UCI Dataset:**

https://archive.ics.uci.edu/dataset/502/online+retail+ii

**Kaggle Mirror:**

https://www.kaggle.com/datasets/mathchi/online-retail-ii-data-set-from-ml-repository

### Dataset Citation

Chen, D. (2012). *Online Retail II*. UCI Machine Learning Repository.

**DOI:** https://doi.org/10.24432/C5CG6D

---

# 4. Dataset Schema

| Column | Description |
|---|---|
| InvoiceNo | Invoice number; invoices beginning with `C` represent cancellations |
| StockCode | Product identifier |
| Description | Product description |
| Quantity | Quantity purchased |
| InvoiceDate | Transaction date and time |
| UnitPrice | Unit price in GBP |
| CustomerID | Customer identifier |
| Country | Customer's country |

---

# 5. Data Quality Assessment

Initial profiling identified:

| Metric | Value |
|---|---:|
| Total Records | 1,067,371 |
| Total Columns | 9 |
| Duplicate Records | 34,335 |
| Missing CustomerID | 243,007 |
| Missing Description | 4,382 |
| Unique Customers | 5,942 |
| Unique Invoices | 53,628 |
| Unique Products | 5,305 |
| Unique Countries | 43 |
| Cancellation Records | 19,494 |
| Negative Quantity Records | 22,950 |
| Zero Quantity Records | 0 |
| Zero Price Records | 6,202 |
| Negative Price Records | 5 |
| Invalid Dates | 0 |

### Cleaning Strategy

The project uses **business-aware data cleaning** rather than blindly deleting unusual records.

- Missing CustomerID → retained where useful for transaction-level analysis
- Missing Description → investigated using available product information
- Cancellation invoices → identified separately
- Negative quantities → analyzed as returns/cancellations
- Duplicate records → investigated and handled
- Zero/negative prices → identified for validation
- Dates → standardized and validated

Revenue was calculated as:

```text
Revenue = Quantity × UnitPrice
```

---

# 6. Analytical Workflow

```text
Raw Data
   ↓
Data Profiling
   ↓
Data Cleaning
   ↓
EDA
   ↓
RFM Segmentation
   ↓
Churn / Inactivity
   ↓
Demand Analysis
   ↓
30-Day Forecast
   ↓
Inventory Planning
   ↓
Power BI Dashboard
   ↓
Business Recommendations
```

---

# 7. Exploratory Data Analysis

EDA focuses on four major business dimensions.

### Sales Performance

- Revenue trends
- Monthly revenue
- Order activity
- Average Order Value

### Product Performance

- Top products by revenue
- Top products by quantity
- Product contribution

### Geographic Performance

- Country-level revenue
- Country-level transaction activity

### Customer Performance

- Customer revenue
- Purchase frequency
- Recency
- Monetary value

---

# 8. Customer Analytics

## RFM Segmentation

Customers are analyzed using:

- **Recency** — how recently the customer purchased
- **Frequency** — how frequently the customer purchased
- **Monetary** — how much revenue the customer generated

RFM segmentation helps identify valuable customers and different engagement levels.

---

# 9. Churn / Inactivity Analysis

Observed churn output:

| Churn | Customers |
|---:|---:|
| 1 | 2,989 |
| 0 | 2,889 |

The analysis supports identification of customers who may require retention attention.

### Potential Actions

- Customer re-engagement
- Targeted retention campaigns
- Personalized offers
- High-value customer monitoring

> Churn labels are analytical/model outputs and should be validated against an organization's actual churn definition before production use.

---

# 10. Product & Demand Analysis

Product analysis focuses on:

- High-volume products
- High-revenue products
- Historical demand
- Product contribution
- Demand concentration

This analysis provides the foundation for demand forecasting and inventory planning.

---

# 11. 30-Day Demand Forecasting

A time-series forecasting workflow was developed to estimate short-term demand.

The forecast includes:

- Daily demand estimates
- Forecast horizon
- Lower forecast bound
- Upper forecast bound

### Forecasting Flow

```text
Historical Demand
       ↓
Time-Series Preparation
       ↓
Forecasting Model
       ↓
30-Day Forecast
       ↓
Inventory Planning
```

Forecast values are planning estimates and should be validated against future actual demand.

---

# 12. Inventory Optimization

Forecast demand was connected to inventory planning concepts:

- Average Daily Demand
- Lead-Time Demand
- Safety Stock
- Reorder Point

Conceptually:

```text
Reorder Point =
Lead-Time Demand + Safety Stock
```

Because actual warehouse stock, supplier lead times, purchase orders, and stock-out information are not included in the source dataset, inventory recommendations are **scenario-based**.

---

# 13. Power BI Dashboard

The final Power BI report contains **four pages**.

## Page 1 — Executive Overview

### Business Question

**How is the business performing?**

### KPIs

- Total Revenue
- Total Orders
- Total Customers
- Total Products
- Average Order Value

### Visuals

- Monthly Revenue Trend
- Revenue by Country
- Top 10 Products by Revenue
- Country Filter

### Purpose

Provides a high-level view of overall business performance.

---

## Page 2 — Customer Intelligence

### Business Question

**Who are our valuable customers and which customers require attention?**

### KPIs

- Total Customers
- Active Customers
- Inactive Customers
- Inactive Rate

### Visuals

- Customer Segment Distribution
- Revenue by Customer Segment
- Inactive Rate by Segment
- Customer Risk Distribution
- High-Value Customers at Risk

### Purpose

Identifies customer value, inactivity, risk, and retention opportunities.

---

## Page 3 — Product & Demand Analysis

### Business Question

**Which products drive demand and what demand should we expect next?**

### KPIs

- Total Products
- Total Quantity
- Average Daily Forecast
- 30-Day Forecast Demand

### Visuals

- Top 10 Products by Quantity
- Historical Product Demand
- 30-Day Demand Forecast
- Product Filter

### Purpose

Supports product prioritization and short-term demand planning.

---

## Page 4 — Inventory Optimization

### Business Question

**How can forecasted demand support replenishment decisions?**

### KPIs

- 30-Day Forecast Demand
- Lead-Time Demand
- Safety Stock
- Reorder Point

### Visuals

- Demand Forecast
- Inventory Recommendation Distribution
- Inventory Planning Recommendations

### Purpose

Connects demand forecasting with replenishment and inventory planning.

---

# 14. Key Business Insights

- Data quality must be addressed before relying on business KPIs.
- Missing CustomerID limits customer-level analysis.
- Cancellations and negative quantities should be treated as meaningful business events.
- RFM segmentation helps prioritize customers based on value and engagement.
- Churn/inactivity analysis can support targeted retention.
- Demand forecasting adds a forward-looking perspective to historical sales analysis.
- Forecast demand can support safety-stock and reorder-point planning.

---

# 15. Business Recommendations

1. Prioritize high-value customers with elevated inactivity risk.
2. Monitor high-revenue and high-volume products.
3. Use the 30-day forecast for short-term demand planning.
4. Review products approaching modeled reorder points.
5. Improve CustomerID, product description, pricing, and duplicate-data quality.
6. Monitor forecast accuracy against future actual demand.
7. Separate cancellations and returns from normal sales KPIs.

---

# 16. Technology Stack

| Category | Tools |
|---|---|
| Programming | Python |
| Data Analysis | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn, Plotly |
| Forecasting | Prophet |
| Business Intelligence | Microsoft Power BI |
| Data Transformation | Power Query |
| Calculations | DAX |
| Development | Jupyter Notebook |
| Version Control | Git / GitHub |

---

# 17. Project Structure

```text
RetailPulse/
│
├── README.md
│
├── Notebooks/
│   ├── Data_Profiling.ipynb
│   ├── Data_Cleaning.ipynb
│   ├── EDA.ipynb
│   ├── RFM_Customer_Segmentation.ipynb
│   ├── Churn_Analysis.ipynb
│   ├── demand_forecasting.ipynb
│   ├── Inventory_Optimization.ipynb
│   └── dashboard_preparation.ipynb
│
├── data/
│   ├── cleaned/
│   ├── eda/
│   ├── forecast/
│   └── dashboard/
│
├── power BI/
│   └── RetailPulse.pbix
│
├── reports/
│   ├── RetailPulse_Business_Problem_Statement.pdf
│   └── RetailPulse_Final_Result_Report.pdf
│
└── images/
    ├── page1_executive_overview.png
    ├── page2_customer_intelligence.png
    ├── page3_product_demand.png
    └── page4_inventory_optimization.png
```

Large datasets are excluded from GitHub using `.gitignore`.

---

# 18. Reproducibility

### Clone Repository

```bash
git clone https://github.com/srinivasu-alavala/RetailPulse_analytics_project.git
```

### Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn plotly prophet jupyter
```

### Download Dataset

Download Online Retail II from:

https://archive.ics.uci.edu/dataset/502/online+retail+ii

Place the dataset in the appropriate local `data/raw/` directory.

### Recommended Notebook Order

1. Data_Profiling.ipynb
2. Data_Cleaning.ipynb
3. EDA.ipynb
4. RFM_Customer_Segmentation.ipynb
5. Churn_Analysis.ipynb
6. demand_forecasting.ipynb
7. Inventory_Optimization.ipynb
8. dashboard_preparation.ipynb

### Power BI

Open:

```text
power BI/RetailPulse.pbix
```

and connect the report to the generated analytical outputs.

---

# 19. Limitations

- Missing CustomerID limits customer-level analysis.
- Inventory recommendations are scenario-based because actual stock and supplier information are unavailable.
- Forecasts require validation against future actual demand.
- Churn output should be aligned with the organization's actual churn definition before production use.

---

# 20. Future Enhancements

- Customer Lifetime Value
- Cohort Analysis
- Market Basket Analysis
- Forecast Accuracy Monitoring
- Automated Power BI Refresh
- SQL Data Warehouse
- Supplier Analytics
- Stock-out Prediction
- Promotion Impact Analysis

---

# 21. Portfolio Description

### RetailPulse — Retail Transaction Analytics & Business Intelligence

Developed an end-to-end retail analytics solution using **Python and Power BI** to transform **1M+ transaction records** into actionable business insights.

Performed:

- Data profiling
- Data cleaning
- Exploratory Data Analysis
- RFM customer segmentation
- Churn/inactivity analysis
- 30-day demand forecasting
- Inventory planning

Built a **four-page Power BI dashboard** covering:

- Executive Performance
- Customer Intelligence
- Product & Demand Analysis
- Inventory Optimization

---

# 22. Project Highlights

| Area | Implementation |
|---|---|
| Dataset | 1M+ real-world transactions |
| Data Quality | Profiling + business-aware cleaning |
| EDA | Sales, product, customer, country analysis |
| Customer Analytics | RFM segmentation |
| Retention | Churn / inactivity analysis |
| Forecasting | 30-day demand forecasting |
| Inventory | Safety stock + reorder point |
| BI | 4-page Power BI dashboard |
| Documentation | Business problem + final result reports |
| Version Control | Git + GitHub |

---

# 23. Author

**Srinivas Alavala**

**Aspiring Data Analyst**

Email: srinivasualavala@gmail.com

GitHub:
https://github.com/srinivasu-alavala/RetailPulse_analytics_project

---

# 24. Dataset Attribution

This project uses the **Online Retail II** dataset created by Daqing Chen and distributed through the UCI Machine Learning Repository.

**Dataset:** Online Retail II

**Source:** UCI Machine Learning Repository

**DOI:** https://doi.org/10.24432/C5CG6D

**License:** CC BY 4.0

For complete dataset documentation, citation, and licensing information, refer to the original UCI repository.

---

> **Disclaimer:** RetailPulse is an analytical portfolio project. Forecasting, churn, and inventory outputs are intended for demonstration and decision-support purposes and should be validated against current operational data before production use.
