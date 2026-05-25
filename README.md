\# Ecommerce Sales SQL Analysis Project



\## Project Overview

This project focuses on analyzing ecommerce sales data using SQL.



The dataset was sourced from Kaggle and analyzed using Microsoft SQL Server Management Studio (SSMS).



The objective of this project was to perform sales analysis, customer analysis, revenue analysis, and payment trend analysis using different SQL concepts.



\---



\## Dataset Information



Dataset Source:

Olist Brazilian Ecommerce Dataset from Kaggle



Dataset Includes:

\- Orders data

\- Customer data

\- Payment data

\- Product information

\- Order status information



\---



\## Tools Used



\- SQL

\- Microsoft SQL Server

\- SSMS

\- GitHub

\- Kaggle Dataset



\---



\## SQL Concepts Used



\- SELECT

\- WHERE

\- GROUP BY

\- ORDER BY

\- HAVING

\- DISTINCT

\- Aggregate Functions

\- INNER JOIN

\- CASE WHEN

\- Common Table Expressions (CTE)

\- Window Functions

\- RANK()



\---



\## Analysis Performed



\### Basic Analysis

\- Total Orders

\- Total Revenue

\- Unique Customers

\- Average Payment

\- Maximum and Minimum Payment



\### Payment Analysis

\- Revenue by Payment Type

\- Top Payment Methods

\- High Value Transactions



\### Customer Analysis

\- Top Customers by Revenue

\- Customers with Multiple Orders

\- Average Revenue Per Customer



\### Time-Based Analysis

\- Monthly Revenue

\- Yearly Orders

\- Yearly Revenue

\- Latest Orders



\### Advanced SQL Analysis

\- Payment Category using CASE WHEN

\- High Value Customers using CTE

\- Customer Ranking using Window Functions



\---



\## Sample SQL Queries



\### Total Revenue



```sql

SELECT SUM(payment\_value) AS total\_revenue

FROM olist\_order\_payments\_dataset;

```



\### Top Customers by Revenue



```sql

SELECT TOP 10 o.customer\_id,

&#x20;      SUM(p.payment\_value) AS total\_revenue

FROM olist\_orders\_dataset o

JOIN olist\_order\_payments\_dataset p

ON o.order\_id = p.order\_id

GROUP BY o.customer\_id

ORDER BY total\_revenue DESC;

```



\---



\## Business Insights



\- Credit card payments generated the highest revenue.

\- A small number of customers contributed significantly higher revenue.

\- Revenue trends changed over different months and years.

\- High-value transactions were limited but contributed major revenue.



\---



\## Project Structure



```text

Ecommerce-Sales-SQL-Analysis

│

├── ecommerce\_sales\_analysis.sql

├── README.md

├── dataset.csv

├── screenshots

│   ├── revenue\_analysis.png

│   ├── customer\_analysis.png

│

└── insights.txt

```



\---



\## Screenshots



Example:

\- Revenue Analysis

\- Customer Ranking

\- Payment Analysis



\---



\## Future Improvements



\- Create Power BI Dashboard

\- Add Data Visualization

\- Perform Product Category Analysis

\- Build Interactive Dashboard



\---



\## Author



SQL Ecommerce Analysis Project by Saksham Chabukswar

