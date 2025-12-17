# SQL Data Warehouse Analytics Project

## Overview

This project is an **end-to-end SQL-based analytics solution** built on a dimensional data warehouse architecture. It transforms transactional sales data into **business-ready insights** using structured fact and dimension tables within a **Gold Layer**.

The project focuses on analytical SQL patterns commonly used by data engineers and analytics engineers, including trend analysis, ranking, segmentation, cumulative metrics, and KPI reporting.

---

### Data Model (Gold Layer)
The analytics layer follows a **Star Schema** design optimized for BI and reporting:

#### Fact Table
- **gold.fact_sales**  
    Stores transactional sales data such as order number, order date, quantity, price, and sales amount.
#### Dimension Tables
- **gold.dim_customers**  
    Customer attributes (name, gender, country, birthdate, customer number).
- **gold.dim_products**  
    Product attributes (product name, category, subcategory, cost).


---

####  1. Exploratory Data Analysis (EDA)
 Scripts 01–04 audit the schema, verify data integrity, and establish the business's "temporal boundaries" (e.g., finding the oldest/youngest customers and the total span of sales history).

---
#### Analytical Modules
Each SQL file addresses a specific analytical pattern used in real-world data analytics.

---
#### 5. Magnitude Analysis
**Purpose**: Understand data distribution across key dimensions.
**Key Insights**:
- Customer distribution by country and gender
- Product distribution by category
- Average product cost per category
- Revenue contribution by category and by customer
- Sales quantity distribution across countries
**Techniques Used**:
- `SUM()`, `COUNT()`, `AVG()`
- `GROUP BY`, `ORDER BY`
---
#### 6. Ranking Analysis
**Purpose**: Identify top and bottom performers.
**Key Insights**:
- Top 5 and bottom 5 products by revenue
- Top 10 customers by revenue 
- Customers with the fewest orders

**Techniques Used**:
- `TOP`
- Window functions: `RANK()`
- Aggregations with flexible ranking logic
---
#### 7. Change Over Time Analysis
**Purpose**: Track trends and seasonality in sales performance.
**Key Insights**:
- Monthly and yearly sales trends
- Customer and quantity growth over time

**Date Handling Techniques**:
- `YEAR()`, `MONTH()`
- `DATETRUNC()`
- `FORMAT()`
---
#### 8. Cumulative Analysis
**Purpose**: Measure performance growth over time.
**Key Metrics**:
- Running total of sales
- Moving average of selling price

**Techniques Used**:
- Window functions: `SUM() OVER()`, `AVG() OVER()`
---
#### 9. Performance Analysis (Year-over-Year)
**Purpose**: Evaluate product performance over time.
**Key Insights**:
- Comparison against historical averages
- Year-over-Year (YoY) sales growth or decline

**Techniques Used**:
- `LAG()` for prior-year comparison
- `AVG() OVER()` for benchmarking
- `CASE` statements for performance labeling

---

#### 10. Data Segmentation Analysis
**Purpose**: Create meaningful business segments.
### Product Segmentation
- Cost-based product buckets (Below 100, 100–500, etc.)
### Customer Segmentation
- **VIP**: ≥ 12 months lifespan and spending > €5,000
- **Regular**: ≥ 12 months lifespan and spending ≤ €5,000
- **New**: < 12 months lifespan
**Techniques Used**:
- `CASE`
- CTE-based segmentation logic
---
#### 11. Part-to-Whole Analysis
**Purpose**: Understand category contribution to total revenue.
**Key Metrics**:
- Category-level revenue contribution
- Percentage of total sales
**Techniques Used**:
- Window aggregation: `SUM() OVER()`
- Percentage calculations
---
## 12. Customer Report (gold.report_customers)
A reusable **analytics view** consolidating customer KPIs.
**Metrics Included**:
- Total orders, sales, quantity, and products
- Customer lifespan and recency
- Average order value (AOV)
- Average monthly spend
**Customer Attributes**:
- Age and age group
- Customer segment (VIP / Regular / New)
This view is designed for **BI dashboards and CRM analytics**.
---
#### 13. Product Report (gold.report_products)
A reusable **product performance view**.
**Metrics Included**:
- Total sales, orders, quantity, customers
- Product lifespan and recency
- Average selling price
- Average order revenue (AOR)
- Average monthly revenue
**Product Segmentation**
- High-Performer
- Mid-Range
- Low-Performer
This view supports **product analytics and performance monitoring**.
---
#### Key SQL Concepts Demonstrated
- Star Schema analytics
- CTE-based transformations
- Window functions for advanced analytics
- KPI engineering in SQL
- Reusable reporting views
---
## Use Cases
- Business Intelligence dashboards (Power BI )
- Executive performance reporting
- Customer and product analytics
---

















This project, **DataWarehouseAnalytics**, is a comprehensive SQL-based end-to-end data engineering and analytics solution. It transforms raw transactional data into a structured **"Gold" Layer** designed for advanced Business Intelligence (BI) and reporting.

---

###  Project Architecture

The project follows a **Star Schema** design to optimize query performance and clarity:
- **Fact Table:** `fact_sales` (Transactions, revenue, and quantities).
- **Dimension Tables:** `dim_customers` and `dim_products` (Descriptive attributes).
- **Final Layer:** Automated SQL Views (`report_customers`, `report_products`) that serve as the single source of truth for stakeholders.
---

###  Analytical Highlights

The 13-script workflow moves beyond simple data storage into deep behavioral and performance analysis:

1. **Exploratory Data Analysis (EDA):** Scripts 01–04 audit the schema, verify data integrity, and establish the business's "temporal boundaries" (e.g., finding the oldest/youngest customers and the total span of sales history).
    
2. **Advanced Window Functions:** The project heavily utilizes SQL window functions like `RANK()` for identifying top performers, and `LAG()` to perform **Year-over-Year (YoY)** growth comparisons.
    
3. **Business Logic Segmentation:**
    
    - **Customer Tiering:** Categorizes users into **VIP**, **Regular**, or **New** based on their spending and "lifespan" (months active).
        
    - **Product Performance:** Segments inventory into **High-Performer**, **Mid-Range**, and **Low-Performer** based on revenue thresholds.
        
4. **Time-Series & Cumulative Insights:** Calculates running totals and moving averages to identify long-term trends and seasonality.
    

---

### 🛠️ Technical Stack

- **Environment:** SQL Server (T-SQL).
- **Key Techniques:** CTEs (Common Table Expressions), Window Functions, Data Aggregation, Schema Design, and `BULK INSERT` for data ingestion.
- **Reporting:** Dynamic Views that calculate complex KPIs like **Recency** (months since last purchase) and **Average Order Value (AOV)** on the fly.

---

###  Business Value
By executing this pipeline, a business can transition from viewing "raw rows" to answering critical questions:
- _Which 5% of customers drive 80% of our revenue?_
- _How does this month’s performance compare to the same month last year?_
- _Which product categories are losing momentum and require marketing intervention?_
