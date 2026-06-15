
# Data Analytics Project 1: Data Cleaning & Preparation
**Organization:** DecodeLabs  
**Cohort/Batch:** 2026 Industrial Training Kit  
**Core Framework:** The Architecture of Data Integrity  
**Tooling Environment:** Microsoft Excel  

---

## 1. Executive Summary
In corporate data ecosystems, poor data quality introduces severe operational risks, costing organizations an estimated 15% to 25% of their annual revenue, with an average global loss of $12.9 million. This project details the data scrubbing pipeline executed to transform a raw, noisy transactional dataset consisting of 1,200 records into a production-ready, verified "Gold Standard" source of truth. 

By prioritizing backend **Data Integrity** over cosmetic visualizations, this cleaning process establishes a rigorous auditing pipeline to ensure all downstream business intelligence, predictive modeling, and corporate dashboards are constructed on a foundation of absolute accuracy.

---

## 2. Core Project Objectives & Deliverables
* **Strategic Gap Resolution:** Resolve missing structural values using explicit analytical data logic to maintain dataset volume.
* **Integrity Auditing:** Enforce a strict unique transaction standard across primary key records to guarantee a 0% duplication error rate.
* **Structural Standardization:** Uniformly align textual capitalization, remove invisible trailing whitespaces, and apply standard international formatting rules.
* **Audit Trail Compilation:** Produce a transparent, permanent change log capturing all pipeline modifications ("*If it isn't documented, it didn't happen*").

---

## 3. Dataset Architecture
* **Source Files:** `OG- Data.csv` (Raw Input) | `cleanedData.csv` (Polished Output)
* **Total Volume:** 1,200 transactional rows
* **Total Target Features:** 14 relational columns
* **Column Schema & Description:**
  1. `OrderID` (Primary Key / Unique Textual Identifier)
  2. `Date` (Temporal chronological marker)
  3. `CustomerID` (Alphanumeric customer entity identifier)
  4. `Product` (Categorical inventory item description)
  5. `Quantity` (Discrete integer counts representing order volumes)
  6. `UnitPrice` (Continuous financial metric representing individual item costs)
  7. `ShippingAddress` (Physical delivery destination string)
  8. `PaymentMethod` (Categorical transaction settlement medium)
  9. `OrderStatus` (Operational processing lifecycle state)
  10. `TrackingNumber` (Unique alphanumeric logistics reference code)
  11. `ItemsInCart` (Discrete integer counts representing items in cart)
  12. `CouponCode` (Categorical promotional text identifier - *Source of Data Gaps*)
  13. `ReferralSource` (Categorical digital acquisition channel)
  14. `TotalPrice` (Computed financial metric representing gross transaction revenues)

---

## 4. Phase-by-Phase Cleaning Methodology

### Phase 1: Strategic Imputation & Missing Value Resolution
An initial diagnostic audit of the raw matrix revealed exactly 309 missing records located exclusively within the `CouponCode` column. 
* **The Treatment Logic:** To preserve the complete profile of all 1,200 purchases, rows were kept intact. The 309 missing parameters were strategically classified and explicitly filled with the descriptive string **`NoCoupon`**. This conversion distinguishes transactions executed without promotional materials from active codes (`SAVE10`, `FREESHIP`, `WINTER15`) without corrupting downstream categorization models.
* **Excel Technical Execution:**
  1. Highlighted the complete boundary range of Column L (`CouponCode`).
  2. Invoked the **Go To Special** dialog widget (`Ctrl + G` -> clicked `Special...`).
  3. Checked the selection bubble for **Blanks** and executed `OK` to lock focus exclusively on the empty cells.
  4. Injected the string string literal `NoCoupon` into the active terminal field and executed **`Ctrl + Enter`** to broadcast the change uniformly across all highlighted gaps simultaneously.

### Phase 2: Primary Key Integrity Audit (One Truth, One Record)
To prevent artificial inflation of metrics and secure transaction uniqueness across the repository, a key safety validation gate was executed.
* **The Treatment Logic:** Individual `OrderID` records must serve as a strict primary key containing zero overlapping fields.
* **Excel Technical Execution:**
  1. Selected Column A (`OrderID`) across all 1,200 records.
  2. Navigated to ribbon: `Home` -> `Conditional Formatting` -> `Highlight Cells Rules` -> `Duplicate Values`.
  3. Applied a high-contrast red fill format to run an immediate visual error check.
  4. The system validated a 0% redundancy rate across the entire range, proving that every record represents an isolated unique event.

### Phase 3: Speak One Language (Standardization Filters)
To transform the dataset into a corporate-ready data asset, rows were put through rigorous text, timeline, and mathematical formatting filters.

#### 3.1 Text Whitespace & Casing Overhaul
Manual inputs frequently inject trailing spaces and random word mutations (e.g., lowercase vs uppercase mix-ups) which break index formulas and pivot grouping pipelines.
* **Excel Technical Execution:**
  1. Generated temporary helper columns adjacent to categorical elements (`Product`, `PaymentMethod`, `OrderStatus`, `ReferralSource`).
  2. Applied a nested text utility function: `=TRIM(PROPER(Cell))` to strip leading/trailing spaces and force proper sentence casing.
  3. Dragged the fill handle downward to flash-fill all rows, copied the updated results, and performed a **Paste as Values (123)** back over the original input parameters to isolate the text.

#### 3.2 Chronological Standard Alignment
Chronological discrepancies disrupt timeline sorting and moving average calculations. The formatting rules require alignment to international specifications.
* **Excel Technical Execution:**
  1. Highlighted Column B (`Date`).
  2. Launched cell configurations (`Ctrl + 1`), navigated to the bottom option, and selected **Custom**.
  3. Programmed the international standard string pattern into the *Type* box: `yyyy-mm-dd`.
  4. Saved changes, guaranteeing perfect chronological uniformity across the ledger.

#### 3.3 Numeric Currency Precision
Continuous currency numbers must mirror an absolute uniform precision profile to confirm clean mathematical aggregations.
* **Excel Technical Execution:**
  1. Selected columns F (`UnitPrice`) and N (`TotalPrice`) simultaneously using the `Ctrl` selector modifier.
  2. Opened formatting configurations via `Ctrl + 1` and applied the **Number** option.
  3. Configured the cell options to lock data strictly to **2 decimal places**.

---

## 5. Completed Pipeline Change Log
This repository log serves as the verified audit trail ensuring every structural adjustment is formally documented.

| Change ID | Feature Target | Action Implemented | Data/Statistical Justification | Status |
| :--- | :--- | :--- | :--- | :--- |
| **CR001** | `CouponCode` | Isolated blanks via Go To Special and mapped them to `NoCoupon`. | Restored 309 rows; defended dataset from drop bias and explicit categorical skewing. | **Resolved** |
| **CR002** | `OrderID` | Deployed Conditional Formatting duplicate filters. | Documented a 0% duplication error rate, securing unique tracking constraints. | **Resolved** |
| **CR003** | `Product`, `OrderStatus`, `PaymentMethod` | Programmed nested `=TRIM(PROPER())` values, pasting outcomes over raw data. | Eliminated invisible trailing/leading whitespaces and normalized random letter casings. | **Resolved** |
| **CR004** | `Date` | Enforced strict custom `yyyy-mm-dd` configuration rules. | Restructured chronological markers to the universal ISO 8601 standard. | **Resolved** |
| **CR005** | `UnitPrice`, `TotalPrice` | Programmed cells to the Number structure restricted to 2 decimal points. | Guaranteed uniform mathematical alignment for downstream financial calculations. | **Resolved** |

---

## 6. Verification & Data Integrity Sign-Off
Following the execution of the Excel data cleaning pipeline, the final `cleanedData.csv` output was put through a final audit sweep. The diagnostic results confirm:
1. **Missing Elements:** Exactly 0 blank cells remain across all 1,200 rows and 14 metrics.
2. **Duplication Error Rate:** Exactly 0.00% primary identifier collisions.
3. **Format Alignment:** 100% compliance with ISO 8601 chronology and 2-decimal financial parameters.

The spreadsheet has successfully transitioned from noisy, raw transactional data into a certified **"Gold Standard"** digital asset, fully satisfying the qualification parameters required to unlock the next analytical module.
