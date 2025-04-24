# 🐊 CORS Data Warehouse Project

This project is developed as part of the interview process for a Business Analyst role at Crocoroos’s Online Retail Store (CORS). The objective is to design and implement a data warehouse using sales data provided through Amazon's portal, enabling CORS to make data-driven decisions for operational efficiency and business growth.

---

## 📝 Project Overview

Crocoroos’s Online Retail Store (CORS) is a specialized e-commerce business selling a wide range of products. Due to the limitations of their current transactional systems and the complexity of analyzing sales data in various formats (database and CSV), a dedicated **data warehouse** solution has been proposed.

### Objectives:
- Develop a dimensional data model suitable for business analytics.
- Integrate transactional data using **SQL Server Integration Services (SSIS)**.
- Load the data into a structured data warehouse.
- Run analytical queries to extract valuable business insights.

---

## 📊 Dimensional Model Design

The data warehouse follows a **star schema** model with a central fact table and multiple dimension tables. The granularity of the fact table is at the **order item level**.

### 🌟 Dimensional Model 2.0
![Dimensional Model](Dimensional%20Model%202.0.png)

---

## 🧱 Dimension Tables

### 🧍‍♂️ DimCustomer
Contains information about CORS customers including region and demographic attributes.

![DimCustomer](Images/DimCustomer.png)

---

### 📅 DimDate
A date dimension table used to analyze data over time (daily, monthly, quarterly, yearly).

![DimDate](DimDate.png)

---

### 📍 DimLocation
Represents geographic data for customers and suppliers to assist in warehouse and logistics planning.

![DimLocation](DimLocation.png)

---

### 📦 DimOrders
Captures metadata related to customer orders.

![DimOrders](DimOrders.png)

---

### 🎮 DimProduct
Holds product-related data including category and pricing.

![DimProduct](DimProduct.png)

---

### 🏭 DimSuppliers
Information about suppliers from whom products are bulk purchased.

![DimSuppliers](DimSuppliers.png)

---

## 📈 Fact Table

### 🧾 FactOrderItem
Records detailed transaction-level data including sales amount, quantity, discounts, and profit.

![FactOrderItem](FactOrderItem.png)

---

## ⚙️ ETL Process (SSIS)

Data from Amazon (in CSV and database formats) is extracted, cleaned, transformed, and loaded using **SQL Server Integration Services (SSIS)**. The ETL pipeline:
- Ensures referential integrity with lookup and data conversion tasks.
- Uses derived columns to calculate revenue and profit.
- Populates all dimension and fact tables in the data warehouse.

---

## 📌 Sample Analytical Queries

```sql
-- Top 5 best-selling products by revenue
SELECT TOP 5 P.ProductName, SUM(F.SalesAmount) AS Revenue
FROM FactOrderItem F
JOIN DimProduct P ON F.ProductKey = P.ProductKey
GROUP BY P.ProductName
ORDER BY Revenue DESC;
