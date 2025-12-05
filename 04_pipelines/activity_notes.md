# Microsoft Fabric Data Pipeline Documentation
## Project: Retail Sales Analytics Pipeline
## File: activity_notes.md
## Purpose: Describe pipeline flow, schedule, dataflow, and notebook references.

---

## 1. Pipeline Purpose

The pipeline automates the end-to-end ETL workflow for the Retail Sales Analytics project.  
It performs the following tasks:

### ✔ 1. Ingest Raw Data
- Copies raw CSV files (sales, products, stores, customers) from `OneLake/Files/raw/`
- Stores them into a structured location inside the Lakehouse
  - `/Tables/raw_sales`
  - `/Tables/raw_products`
  - `/Tables/raw_stores`
  - `/Tables/raw_customers`

---

### ✔ 2. Transform Data Using Notebooks
Runs PySpark notebooks in sequence:

1. **Notebook: ingest_raw_data.ipynb**
   - Reads raw CSVs  
   - Performs schema validation  
   - Stores DataFrames as Delta tables  

2. **Notebook: transform_sales.ipynb**
   - Cleans sales records  
   - Handles missing or invalid values  
   - Converts date formats  
   - Normalizes StoreID and ProductID references  

3. **Notebook: create_dim_fact.ipynb**
   - Builds star schema tables:
     - `dim_products`
     - `dim_stores`
     - `fact_sales`
   - Adds calculated fields like:
     - `SalesAmount = Quantity * UnitPrice`

4. **Notebook: data_quality_checks.ipynb**
   - Verifies:
     - Record counts  
     - Null checks  
     - Referential integrity between dim/fact tables  
   - Logs errors into `/Tables/data_quality_log`

---

### ✔ 3. Update SQL Endpoint Metadata
- Refreshes Lakehouse SQL endpoint  
- Ensures Power BI models pick up latest schema  

---

### ✔ 4. Load Data into Analytics Layer
- Makes tables available for Power BI:
  - `fact_sales`
  - `dim_products`
  - `dim_stores`

---

## 2. Pipeline Sequence (End-to-End Flow)

1. **Copy Data Activity**
2. **Notebook Activity: ingest_raw_data**
3. **Notebook Activity: transform_sales**
4. **Notebook Activity: create_dim_fact**
5. **Notebook Activity: data_quality_checks**
6. **SQL Endpoint Refresh**
7. **Power BI Dataset Refresh**

---

## 3. Pipeline Schedule

### **Frequency**
Daily

### **Time**
06:00 AM IST

### **Trigger Details**
- Trigger type: **Scheduled**
- Retry Count: **3**
- Retry Delay: **5 minutes**
- On Failure:
  - Log error to `Pipeline_Error_Log`
  - Send email notification (optional)

---

## 4. Dataflow Information

Although this project relies primarily on Notebooks and Pipelines, a Dataflow Gen2 is used for:

### ✔ Dataflow: df_clean_products
- Loads product catalog from CSV
- Removes duplicates
- Standardizes category names
- Outputs cleaned table to:
  - `/Tables/dim_products_staging`

### ✔ Dataflow: df_clean_stores
- Validates store names, city, and state
- Removes invalid or unknown store values
- Outputs table to:
  - `/Tables/dim_stores_staging`

These staging tables are consumed by the `create_dim_fact` notebook.

---

## 5. Notebook References

### 📌 Notebook 1: `ingest_raw_data.ipynb`
- Reads raw CSVs  
- Writes Delta tables under `/Tables/raw_*`

### 📌 Notebook 2: `transform_sales.ipynb`
- Cleans and standardizes sales data  
- Adds derived columns  
- Stores clean table as `/Tables/clean_sales`

### 📌 Notebook 3: `create_dim_fact.ipynb`
- Creates Star Schema:
  - `dim_products`
  - `dim_stores`
  - `fact_sales`

### 📌 Notebook 4: `data_quality_checks.ipynb`
- Row count validation  
- Null checks  
- Foreign key validation  
- Logs issues in `data_quality_log`

---

## 6. Summary

This pipeline ensures:

- Automated ETL workflow  
- Reliable daily refresh  
- Clean and modeled data for analytics  
- Consistent schema for Power BI  
- Scalable architecture using Microsoft Fabric Lakehouse

---

End of file.
