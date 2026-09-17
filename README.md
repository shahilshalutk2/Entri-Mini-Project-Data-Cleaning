# Car Sales Data Cleaning & Preprocessing Project

**Author:** Shahil Shalu TK  
**Tool Used:** Microsoft Excel / Power Query  
**Date:** September 2026  

---

## 1. Project Overview
This project focuses on cleaning, structuring, and standardizing a raw car sales transactional dataset in Microsoft Excel to prepare it for exploratory data analysis (EDA), reporting dashboards, and visualization. The raw data contained structural inconsistencies, character encoding artifacts, truncated categorical strings, missing entries, and outlier/default numeric values.

---

## 2. Data Preparation & Filtering Workflow

1. **Chronological Sorting:**
   * Sorted the dataset ascending by the `Date` column to establish a consistent timeline from earliest to latest transactions.

2. **Temporal Scope Filtering (2023 Cohort):**
   * Filtered the date records and removed all historical transactions from the year **2022**.
   * Retained exclusively sales records spanning from **January 2, 2023** to **December 31, 2023** (13,261 rows).

3. **Feature Selection & Column Pruning:**
   * Removed the column `Dealer_No` (or redundant dealer identifier attributes) to reduce noise, prevent cardinality issues, and streamline downstream visual modeling.

4. **Encoding & Text Artifact Remediation:**
   * **Engine Column:** Cleaned hidden byte sequence artifacts (`Â ` non-breaking spaces), standardizing all occurrences of `DoubleÂ Overhead Camshaft` to `Double Overhead Camshaft`.
   * **Company Column:** Standardized truncated manufacturer names, replacing `Mercedes-B` with `Mercedes-Benz`.
   * **Customer Name Column:** Identified placeholder strings (`"Empty"`) and replaced them with true blank (`null`) values, ensuring valid customer aggregations without deleting transaction rows.
   * **Whitespace Trimming:** Stripped accidental leading and trailing whitespace across all text/categorical fields.

5. **Data Formatting & Categorization:**
   * **Phone Column:** Converted raw 7-digit numeric entries into standard telephone text formats (`###-####`).
   * **Currency & Value Fields:** Formatted `Annual Income` and `Price ($)` using clean currency formatting with thousand/lakh separators.
   * **Income Quality Audit (`Income_Status`):** Added a conditional audit column flagging placeholder values (`13500`) as `"Unverified / Default"` versus authentic reported figures (`"Verified"`), preventing skewed statistical averages.

---

## 3. Data Dictionary (Cleaned Schema)

| Field Name | Data Type | Description |
| :--- | :--- | :--- |
| `Car_id` | Text | Unique identifier for each car sale transaction |
| `Date` | Date | Date of vehicle sale (YYYY-MM-DD) |
| `Customer Name` | Text | Name of the purchasing customer (blanks for missing) |
| `Gender` | Text | Customer gender (`Male` / `Female`) |
| `Annual Income` | Numeric / Currency | Reported customer annual income |
| `Dealer_Name` | Text | Name of the dealership handling the transaction |
| `Company` | Text | Vehicle manufacturer brand name |
| `Model` | Text | Specific car model name |
| `Engine` | Text | Engine configuration (`Overhead Camshaft` / `Double Overhead Camshaft`) |
| `Transmission` | Text | Transmission type (`Auto` / `Manual`) |
| `Color` | Text | Exterior body color |
| `Price ($)` | Numeric / Currency | Vehicle purchase price |
| `Body Style` | Text | Vehicle body classification (SUV, Sedan, Hatchback, etc.) |
| `Phone` | Text | Formatted 7-digit customer contact number (`###-####`) |
| `Dealer_Region` | Text | Geographical region of the dealership |
| `Income_Status` | Text | Quality flag: `Verified` vs `Unverified / Default` |

---

## 4. Key Takeaways & Usage Notes
* **Average Income Calculations:** When aggregating customer income metrics, filter by `Income_Status = "Verified"` to avoid downward skew caused by the 2,941 default `$13,500` entries.
* **Compatibility:** The resulting clean workbook is structured as a single flat table ready for immediate consumption in Excel Pivot Tables, Power BI, or Python/Pandas workflows.
