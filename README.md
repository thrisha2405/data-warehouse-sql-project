#Data Warehouse and Analytics Project

## 1. Project Architecture & Framework
This project implements a modern **3-Layer Medallion Architecture** using SQL Server to ingest, clean, and model operational business data. The pipeline is designed to handle messy, siloed data from two distinct corporate sources (ERP and CRM systems) and process it into an analytics-ready warehouse.

### The Three Infrastructure Layers:
* **Bronze Layer (Raw):** Ingests flat CSV text files from the source systems exactly as-is. No modifications are made here to preserve absolute data lineage and allow for data reprocessing if needed.
* **Silver Layer (Cleaned & Normalized):** The core data engineering layer. This layer runs SQL scripts to handle missing keys, standardize text casing, rectify broken date formats, and deduplicate overlapping records between the ERP and CRM systems.
* **Gold Layer (Business Ready):** Structures the cleansed data into a highly optimized dimensional model tailored for rapid business intelligence querying and reporting.

---

## 2. Data Modeling (The Star Schema)
To deliver high-performance reporting capabilities for analytical teams, the flat transactional data in the Silver layer is transformed into a **Star Schema** within the Gold Layer. This structure removes operational overhead and minimizes complex table joins.

* **Fact Table:** `fact_sales` (Tracks core operational metrics: revenues, transactional units, prices, and relational foreign keys).
* **Dimension Tables:**
  * `dim_customers` (Deduplicated, uniform client profiles combined across systems).
  * `dim_products` (Standardized product catalog descriptions, cost tracking, and indexing).
  * `dim_date` (Pre-calculated calendar mapping to enable seamless time-series business analysis).

---

## 3. Engineering Challenges & Transformations Solved
The SQL transformation scripts in this repository actively resolve common production data quality issues:
* **Source System Consolidation:** Blended conflicting schemas from independent operational pipelines into single-truth dimension tables.
* **Data Quality Scrubbing:** Isolated NULL values, trimmed trailing whitespaces, and cast text fields to unified database data types.
* **Performance Readiness:** Created structural constraints and clean keys to ensure final analytical queries execute efficiently.

---

## 4. Business Value & Analytical Insights
With the Gold layer structured, the warehouse easily answers critical business performance questions using optimized SQL views and queries:
* **Customer Behavior:** Tracking purchase frequencies and identifying high-value customer acquisition segments.
* **Product Performance:** Identifying the highest-grossing inventory items and regional demand fluctuations.
* **Sales Trends:** Calculating revenue growth performance metrics month-over-month.


