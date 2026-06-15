# Data Analytics Project 3: SQL Data Analysis & ETL Pipeline

## Project Overview
Welcome to **Project 3: SQL Data Analysis**, an extraction phase milestone completed for the **DecodeLabs Industrial Training Track **. 

Moving beyond flat spreadsheets, this project serves as a definitive milestone to master **Querying for Truth**. It demonstrates the fundamental art of writing structured queries to filter, group, and aggregate raw transactional data into high-value business intelligence. 

By mapping visual steps in **Excel Power Query** directly to relational database logic (`SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`), this repository contains a complete pipeline that ingests a raw dataset of **1,200 transactions**, executes an intense data cleaning layer, and transforms the raw records into 6 distinct analytical matrices ready for executive decision-making.

---

## Core Analytics Database Schema
The analytical queries run against a transactional schema containing the following critical attributes:
* `OrderID` (Object - Unique Key)
* `Date` (DateTime - Chronological stamp spanning Jan 2023 – Jun 2025)
* `CustomerID` (Object)
* `Product` (Object - Categorical)
* `Quantity` (Integer)
* `UnitPrice` (Decimal/Currency)
* `TotalPrice` (Decimal/Currency - Primary financial aggregation metric)
* `OrderStatus` (Object - Pipeline status tracking)
* `CouponCode` (Object - Promotional identifiers)
* `PaymentMethod` (Object)
* `ReferralSource` (Object - Marketing channel tracking)

---
## File Deliverable Layout

* orignal-data - Raw baseline transactional ingest tracking log sheet.
* CleanedData - Normalized, transformed data layer mapping clean database data types and standardized uppercase records.
* Coupon_Performance - Grouped analytical view evaluating promotional metrics.
* Product_Insights - Grouped analytical view displaying gross inventory value.
* Order_Health - Pipeline overview detailing status volume profiles.
* Count by Payment Method - Consumer operational behavior summary table.
* Referral Source - Inbound marketing attribution revenue leaderboard.
* Sales_Trends - Chronological chronological dataset charting revenue changes over time.

---

## Technical Pipeline Workflow

### Phase 1: Data Cleaning & ETL (The Relational Schema Framework)
Before querying for data insights, an intensive schema preparation protocol was developed within Power Query to ensure total mathematical and data type integrity:
1. **Data Type Enforcement:** Forced column attributes to strict database rules (e.g., `Date` column cast to explicit **Date**, `Quantity` to **Whole Number**, and financial attributes to **Currency**).
2. **String Standardization:** Transformed all textual attributes (`Product`, `PaymentMethod`, `OrderStatus`) into consistent **UPPERCASE** and applied `Trim` properties to strip trailing white spaces which break string filtering logic.
3. **Null Value Rectification:** Located 309 missing parameters within the `CouponCode` metric and replaced missing records with a standardized `'NOCOUPON'` categorical value to prevent data skewing during aggregation tasks.

### Phase 2: Relational Query Logic Execution (`GROUP BY` / `ORDER BY`)
Using referenced query dependencies, the cleaned transactional data was extracted into five highly concentrated summary tables matching foundational database queries:

#### Query 1: Promotional Coupon Performance Analysis
* **Database Concept:** Clustered grouping, record aggregation (`COUNT(*)`, `SUM()`, `AVG()`), and multi-column ranking (`ORDER BY DESC`).
* **SQL Blueprint:**
```sql
SELECT 
    CouponCode,
    COUNT(OrderID) AS Total_Orders,
    SUM(TotalPrice) AS Total_Revenue,
    AVG(TotalPrice) AS Average_Order_Value
FROM CleanedData
GROUP BY CouponCode
ORDER BY Total_Revenue DESC;
```
#### Query 1: Promotional Coupon Performance Analysis
* **Database Concept:** Clustered grouping, record aggregation (`COUNT(*)`, `SUM()`, `AVG()`), and multi-column ranking (`ORDER BY DESC`).
* **SQL Blueprint:**
```sql
SELECT 
    CouponCode,
    COUNT(OrderID) AS Total_Orders,
    SUM(TotalPrice) AS Total_Revenue,
    AVG(TotalPrice) AS Average_Order_Value
FROM CleanedData
GROUP BY CouponCode
ORDER BY Total_Revenue DESC;
```
#### Query 2: Product Performance Metrics
* **Database Concept:** Inventory aggregation mapping and pipeline volume calculation.
* **SQL Blueprint:**
```sql
SELECT 
    Product,
    SUM(TotalPrice) AS Product_Revenue
FROM CleanedData
GROUP BY Product
ORDER BY Product_Revenue DESC;
```
#### Query 3: Operational Pipeline & Fulfillment Health
* **Database Concept:** Assessing transaction integrity to track logistics distributions.
* **SQL Blueprint:**
```sql
SELECT 
    OrderStatus,
    COUNT(*) AS Status_Count
FROM CleanedData
GROUP BY OrderStatus;
```
#### Query 4: Payment Method Volumetric Analysis
* **Database Concept:** Basic string categorical bucketing and order profiling.
* **SQL Blueprint:**
```sql
SELECT 
    PaymentMethod,
    COUNT(*) AS Order_Count
FROM CleanedData
GROUP BY PaymentMethod
ORDER BY Order_Count DESC;
```
#### Query 5: Marketing Referral Revenue Stream Ranking
* **Database Concept:** Dynamic marketing channel return-on-investment (ROI) tracking.
* **SQL Blueprint:**
```sql
SELECT 
    ReferralSource,
    SUM(TotalPrice) AS Referral_Revenue
FROM CleanedData
GROUP BY ReferralSource
ORDER BY Referral_Revenue DESC;
```
#### Query 6: Revenue Over Time Trend
* **Database Concept:** Date-truncation grouping to isolate monthly macro sales patterns.
* **SQL Blueprint:**
```sql
SELECT 
    DATE_TRUNC('month', Date) AS Start_of_Month,
    SUM(TotalPrice) AS Monthly_Revenue
FROM CleanedData
GROUP BY DATE_TRUNC('month', Date)
ORDER BY Start_of_Month ASC;
```

### Technologies Mastered
*   Excel Power Query: Used to build automated, reproducible data processing steps, clean values, and configure multi-variable aggregation matrices.

*   Relational Query Concepts: Translating real-world business objectives into structured statements (SELECT, WHERE, GROUP BY, ORDER BY, and aggregate functions like SUM, COUNT, AVG).

*   Query Folding & Logic Mapping: Demonstrating how graphical interface steps perfectly replicate SQL database execution engines under the hood.

