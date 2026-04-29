# 🛒 Superstore Sales Analysis
### SQL Project using PostgreSQL

**Author:** Uzma Khan  
**Tool Used:** PostgreSQL, pgAdmin  
**Dataset:** Sample Superstore (9,000+ orders)

---

## 📌 Project Overview

This project analyzes a retail superstore dataset using SQL.
The goal is to uncover insights around sales performance, profit trends,
regional analysis, and customer behavior using real-world data.

---

## 🗂️ Dataset

| Column | Description |
|---|---|
| order_id | Unique order identifier |
| order_date | Date the order was placed |
| ship_date | Date the order was shipped |
| ship_mode | Shipping method used |
| customer_name | Name of the customer |
| segment | Customer segment (Consumer, Corporate, Home Office) |
| region | Geographic region (East, West, North, South) |
| category | Product category |
| sub_category | Product sub-category |
| product_name | Name of the product |
| sales | Revenue from the order |
| quantity | Number of units ordered |
| discount | Discount applied |
| profit | Profit from the order |

---

## 📁 File Structure

```
superstore-sql-analysis/
│
├── README.md
├── schema.sql              ← CREATE TABLE query
├── queries/
│   ├── exploration.sql     ← Basic exploration queries
│   ├── sales_analysis.sql  ← Sales and profit queries
│   └── window_functions.sql ← RANK, LAG, ROW_NUMBER queries
```

---

## 🔍 Queries Covered

### 1. Exploration
- Total row count
- Date range of orders
- Distinct regions and categories

### 2. Sales Analysis
- Total sales and profit by region
- Top 10 products by sales
- Sales by category and sub-category
- Monthly sales trend
- Most profitable customers
- Loss-making orders
- Sales by customer segment
- Average discount by region

### 3. Window Functions
- RANK() — Top products by sales
- RANK() with PARTITION — Best product in each category
- LAG() — Month over month sales comparison
- SUM() OVER — Running total of sales over time
- ROW_NUMBER() — Each customer's order history
- DENSE_RANK() — Regions ranked by profit

---

## 📊 Key Findings

> *(To be updated after running queries)*

- 🏆 **Top Region:** West had the highest total sales
- 📦 **Top Category:** Technology was the most profitable category
- 📉 **Loss Orders:** Several orders with high discounts resulted in negative profit
- 👤 **Top Customer:** Tamara Chand was the most profitable customer
- 📈 **Sales Trend:** Sales showed seasonal growth pattern over the years

---

## 💡 Sample Query — Top 10 Products by Sales

```sql
SELECT product_name,
    SUM(sales) AS total_sales
FROM superstore
GROUP BY product_name
ORDER BY total_sales DESC
LIMIT 10;
```

> *(Add screenshot of result here)*

---

## 💡 Sample Query — Month Over Month Growth

```sql
WITH monthly AS (
    SELECT DATE_TRUNC('month', order_date) AS month,
        SUM(sales) AS total_sales
    FROM superstore
    GROUP BY month
)
SELECT month,
    total_sales,
    LAG(total_sales) OVER (ORDER BY month) AS previous_month_sales
FROM monthly
ORDER BY month;
```

> *(Add screenshot of result here)*

---

## 🚀 How to Run

1. Install PostgreSQL and pgAdmin
2. Create a database
3. Run `schema.sql` to create the table
4. Import `Sample - Superstore.csv` using the COPY command:
```sql
SET datestyle = 'ISO, MDY';

COPY superstore
FROM 'C:\Sample - Superstore.csv'
DELIMITER ','
CSV HEADER;
```
5. Run any query from the `queries/` folder in pgAdmin Query Tool

---

## 📬 Connect with Me

- GitHub: github.com/uzma-khan
- LinkedIn: linkedin.com/in/uzma-khan
