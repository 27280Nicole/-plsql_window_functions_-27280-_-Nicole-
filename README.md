# Names: Umutoniwase Nicole
# ID:27280
# PL assignment


# -plsql_window_functions_-27280-_-Nicole-


# Business Context

A supermarket company sells various products to customers across different regions and records daily sales transactions.

# Data Challenge

The supermarket management lacks detailed insights into product performance, regional sales trends, and customer purchasing behavior. Without analytical reporting, it is difficult to identify top-selling products, track sales growth over time, and segment customers based on spending.

# Expected Outcome

Use SQL JOINs and Window Functions to analyze sales data, identify high-performing products and regions, monitor sales trends, and segment customers to support data-driven business decisions.


# Success Criteria

The success of this analysis will be measured using the following five (5) analytical goals, each implemented using SQL window functions:

Identify the top 5 best-selling products per region
Use the RANK() window function to rank products based on total sales revenue within each region, enabling the business to understand which products perform best in different markets.

Calculate running monthly sales totals
Use SUM() OVER() with a time-based window to compute cumulative monthly sales, helping management track sales growth trends over time.

Measure month-over-month sales growth
Use LAG() and LEAD() functions to compare current month sales with the previous and next months, allowing identification of growth patterns and seasonal fluctuations.

Segment customers into spending quartiles
Use NTILE(4) to classify customers into four spending groups (Premium, Gold, Silver, Bronze) based on total purchase amounts, supporting targeted marketing strategies.

Compute three-month moving average of sales
Use AVG() OVER() with a rolling window frame to smooth short-term fluctuations and highlight longer-term sales trends for improved forecasting.



# Database Schema


CUSTOMERS
-------------------------------------------------
customer_id (PK)
customer_name
region
registration_date



PRODUCTS
-------------------------------------------------
product_id (PK)
product_name
category
price



SALES
-------------------------------------------------
sale_id (PK)
customer_id (FK → CUSTOMERS.customer_id)
product_id (FK → PRODUCTS.product_id)
sale_date
quantity
total_amount


RELATIONSHIPS
-------------------------------------------------
CUSTOMERS (1) ────< (M) SALES
PRODUCTS  (1) ────< (M) SALES


# SQL JOINs Implementation

# INNER JOIN
Retrieve transactions with valid customers and products
<img width="632" height="646" alt="image" src="https://github.com/user-attachments/assets/482b951f-77ac-4047-ab8c-80417616c31a" />

Business Interpretation

This query shows only completed sales where both the customer and product exist in the system. It helps the business analyze valid transactions and ensures data integrity across related tables. This is useful for revenue reporting and operational analysis.

# LEFT JOIN
customers who never made a purchase
<img width="630" height="602" alt="image" src="https://github.com/user-attachments/assets/64d7be4d-f972-42ff-b32a-3b6b7e2bb763" />

# Business Interpretation:

Customers listed here have never made a purchase. This helps the business identify inactive customers for marketing campaigns.

# RIGHT JOIN
Products with No Sales
<img width="657" height="467" alt="image" src="https://github.com/user-attachments/assets/2d1fe1bd-6f60-4346-9083-6ef0cbeec099" />

# Business Interpretation

The query returned no rows, indicating that all products have been sold at least once. This suggests full product engagement with no inactive inventory during the period analyzed.

# FULL OUTER JOIN 
customers and products including unmatched
<img width="821" height="666" alt="image" src="https://github.com/user-attachments/assets/a5db4aa9-b9e8-4635-a3e6-10daf7b7d81a" />

# Business Interpretation

Combines all customers and products including unmatched records. Useful for a complete overview of customers and inventory.

# SELF JOIN  
customers in the same region
<img width="782" height="521" alt="image" src="https://github.com/user-attachments/assets/73c9dc62-c463-4b83-9b70-b60e21af7b94" />

# Business Interpretation

Shows which customers belong to the same region. This can help with regional promotions and grouping strategies.


# Ranking Functions

ROW_NUMBER(), RANK(), DENSE_RANK(), PERCENT_RANK()
Use case: Top customers by total revenue

<img width="815" height="577" alt="image" src="https://github.com/user-attachments/assets/02fe9f6c-2994-421c-8a22-15fad389fac1" />

# Interpretation 
This query ranks customers based on total revenue generated. ROW_NUMBER assigns a unique position, RANK and DENSE_RANK handle ties differently, while PERCENT_RANK shows each customer’s relative position. This helps identify top-performing customers.

# Aggregate Window Functions

SUM(), AVG(), MIN(), MAX()
# Use case: Running totals and trends
Frames: ROWS and RANGE

# Running Monthly Sales Total
<img width="685" height="643" alt="image" src="https://github.com/user-attachments/assets/b23bc22b-da68-4297-be97-ca2ffb707c0d" />

# Interpretation
This query calculates cumulative sales over time and a three-transaction moving average. Running totals show overall growth, while the moving average smooths short-term fluctuations to reveal sales trends.

# Navigation Functions

LAG(), LEAD()
# Use case: Month-over-month growth

<img width="896" height="653" alt="image" src="https://github.com/user-attachments/assets/0437ee90-ed52-485b-afd5-e747311fc1ea" />

# Interpretation
This query compares sales amounts across consecutive periods. LAG shows previous sales, LEAD shows upcoming sales, and the difference highlights growth or decline between periods.

# Distribution Functions

NTILE(4), CUME_DIST()
# Use case: Customer segmentation

<img width="730" height="601" alt="image" src="https://github.com/user-attachments/assets/0ecaae96-cd40-4994-a0e2-8addb2092991" />

# Interpretation
This query segments customers into four revenue-based quartiles. NTILE categorizes customers into performance groups, while CUME_DIST shows cumulative contribution, supporting targeted marketing strategies.

## Results Analysis

### 1. Descriptive Analysis (What happened?)
The analysis shows how customer purchases and product sales are distributed across different regions. Some customers generated higher total revenue, while certain products were sold more frequently than others. The running total revealed a steady increase in overall sales over time.

### 2. Diagnostic Analysis (Why did it happen?)
Higher revenue was mainly driven by repeat customers and higher-priced coffee products. Customers from North appeared more frequently in sales records, indicating stronger demand in that region. Product pricing and customer purchasing behavior significantly influenced revenue ranking.

### 3. Prescriptive Analysis (What should be done next?)
The business should focus on high-value customers through loyalty programs and targeted promotions. Expanding marketing efforts in lower-performing regions may increase sales. Additionally, stock planning should prioritize top-performing coffee products to maximize revenue.


## References
1.Oracle PL/SQL Documentation

2.PostgreSQL Window Functions

3.SQL Shack – Window Functions 

4.Mode Analytics – SQL Window Functions

5.Stack Overflow discussions on RANK, NTILE

6.Academic paper: “Sales Analytics Using SQL Window Functions”

7.Medium article: “Customer Segmentation in SQL”

8.TutorialsPoint – SQL Aggregate & Ranking Functions

9.Kaggle example datasets for retail sales analytics

10.Course lecture notes

## Integrity Statement

All sources were properly cited. Implementations and analysis represent original work. No AI generated content was copied without attribution or adaptation.

















