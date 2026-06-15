# Data Analytics Project 2: Exploratory Data Analysis (EDA)

**Organization:** DecodeLabs  
**Cohort/Batch:** 2026 Industrial Training Kit  
**Core Framework:** Exploratory Data Analysis & Statistical Profiling  
**Tooling Environment:** Microsoft Excel  

---

## 📌 Project Overview
This repository showcases the implementation of clean data architecture, mathematical profiling, and multi-dimensional reporting arrays over an e-commerce audit dataset. The project processes 1,200 unique records spanning multiple fiscal years to uncover critical operational performance insights across product portfolios, marketing campaigns, customer retention rates, and fulfillment pipelines.

---

## 📁 Repository Structure
* **`Task 02 -sunai.xlsx`** — Master workbook containing raw data loops, data engineering staging, descriptive stats, and interactive dashboard views.
* **`Task 02 -sunai.xlsx - CleanedData.csv`** — Cleaned baseline transaction log with engineered customer segments.
* **`Task 02 -sunai.xlsx - Summary Statistics.csv`** — Central descriptive data profiling layer.
* **`Task 02 -sunai.xlsx - PivotTables.csv`** — Aggregated multi-dimensional business intelligence matrices.

---

## 🛠️ Data Architecture & Cleaning Staging
The dataset moves through systematic pipeline rules from the unformatted original data tab into a validated reporting table in the `CleanedData` worksheet before reaching any analytics visualization.

### Applied Data Transformations:
* **Handling Structural Sparsity (`CouponCode`):** Imputed missing/null coupon rows with a uniform identifier string (`"NoCoupon"`). This prevents Excel's Pivot engine from clustering sparse records under broken, empty rows.
* **Feature Engineering (`IsRepeatBuyer`):** Synthesized user purchase history profiles to create a binary cohort column (`One-Time` vs. `Repeat`) for customer retention analysis.
* **Logistical Validation Check:** Isolated and segmented order records across their actual execution cycles (`Delivered`, `Shipped`, `Pending`, `Cancelled`, `Returned`) to split active revenue streams from cash flow leakage.

### Complete Data Dictionary & Staging Schema

| Attribute Column | Data Type | Field Profile & Relevance | Engineering Action Applied |
| :--- | :--- | :--- | :--- |
| **OrderID** | Text / Primary Key | Unique transaction trace alphanumeric key | Checked for duplicates and empty fields |
| **Date** | Date (YYYY-MM-DD) | Temporal anchor for tracking seasonality changes | Coerced variant inputs into standardized date structures |
| **CustomerID** | Text / Foreign Key | Unique identifier for the customer profile | Cross-referenced for loyalty recurrence counts |
| **Product** | Categorical String | Product portfolio categories (7 core SKUs) | Standardized taxonomy names across all rows |
| **Quantity** | Discrete Integer | Unit depth purchased per individual transaction | Applied boundaries ensuring integers $>0$ |
| **UnitPrice** | Continuous Currency | Baseline catalog price per individual unit | Standardized floating points for currency layout |
| **PaymentMethod** | Categorical String | Transaction checkout channel chosen by customer | Mapped into 5 clean, standard processing options |
| **OrderStatus** | Categorical String | Current logistical staging step of the transaction | Indexed for dynamic revenue risk sub-filtering |
| **TrackingNumber** | Alphanumeric Text | Supply-chain logistics item tracking code | Validated pattern consistency across fields |
| **ItemsInCart** | Discrete Integer | Total volume basket size inside the order checkout | Verified integrity against quantitative variables |
| **CouponCode** | Categorical String | Applied promotional marketing campaign flag | Replaced null or blank entries with `"NoCoupon"` |
| **ReferralSource** | Categorical String | Inbound customer acquisition channel trace | Isolated channel attribution parameters for ROI views |
| **TotalPrice** | Continuous Currency | Aggregate transaction revenue volume ($Qty \times UnitPrice$) | Truncated calculation anomalies to exactly 2 decimals |
| **IsRepeatBuyer** | Categorical (Derived) | Engineered customer loyalty feature | Built using lookup evaluation metrics on order histories |

---

## 📊 Summary Statistics & Distribution Profiling
A descriptive data profiling analysis was run against the master revenue field (`TotalPrice`) to extract baseline distribution behavior:

* **Total Row Population:** 1,200 Validated Transactions
* **Minimum Order Value:** \$11.39
* **Maximum Order Value:** \$3,456.40
* **Mean Order Value (Average):** \$1,053.97
* **Median Order Value (Center of Gravity):** \$823.62
* **Standard Deviation:** \$819.86
* **Interquartile Range (IQR):** \$1,167.96
* **First Quartile (Q1):** \$410.52
* **Third Quartile (Q3):** \$1,578.48

### Distribution Insights:
The significant right-skew gap between the median (\$823.62) and the mean (\$1,053.97), combined with a high standard deviation (\$819.86), confirms a heavy-tailed transaction distribution. This reveals that revenue is strongly influenced by large commercial multi-item basket checkouts, showing why simple averages fail to tell the full operational narrative without multi-dimensional pivot matrix filters.

---

## 🗂️ Pivot Table Reporting Architecture
The reporting layer inside the `PivotTables` tab maps out structured matrices optimized for multi-dimensional business intelligence tracking:

### 1. Coupon Impact Matrix
* **Objective:** Measures performance across promotion codes (`SAVE10`, `WINTER15`, `FREESHIP`, `NoCoupon`).
* **KPIs Tracked:** Sum of item quantities, total transaction counts, and average customer order values (e.g., `FREESHIP` pacing at a premium average checkout size of \$1,070.41).
* **Strategic Value:** Monitors margin compression levels to ensure discounts drive scaling unit volume instead of decreasing net order values.

### 2. Product Revenue Performance
* **Objective:** Dissects revenue velocities across core product categories (`Chair`, `Printer`, `Tablet`, `Desk`, `Laptop`, `Monitor`, `Phone`).
* **KPIs Tracked:** Aggregated gross sales numbers (e.g., `Chair` and `Printer` both crossing \$195,600+ in performance limits).
* **Strategic Value:** Highlights primary cash engines vs. low-volume items to streamline inventory and product stocking patterns.

### 3. Customer Acquisition Attribution
* **Objective:** Traces generated revenue back to original digital acquisition touchpoints (`Instagram`, `Facebook`, `Google`, `Email`, `Referral`).
* **KPIs Tracked:** Total transactional volume sales alongside aggregate revenue production.
* **Strategic Value:** Pinpoints top performing marketing funnels to support optimization of marketing budget allocations.

### 4. Financial Time-Intelligence View
* **Objective:** Evaluates transaction logs across distinct historical annual horizons (2023, 2024, 2025).
* **KPIs Tracked:** Year-over-Year (YoY) revenue pacing and distribution counts.
* **Strategic Value:** Uncovers baseline performance growth trends and flags seasonal demand cycles.

---

## 📈 Strategic Enhancement Recommendations
To upgrade this analytics architecture into an advanced, automated reporting framework, execute the following system upgrades:

* **Calculate True Net Revenue:** Introduce an automated column to calculate net transaction totals based on specific discount definitions using nested conditional formulas:
  ```excel
  =IF(CouponCode="SAVE10", (Quantity*UnitPrice)*0.9, IF(CouponCode="WINTER15", (Quantity*UnitPrice)*0.85, Quantity*UnitPrice))
