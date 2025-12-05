# 📌 Retail Analytics Pipeline using Microsoft Fabric

## 🔍 Overview

This project demonstrates an end-to-end **Data Engineering pipeline** built using **Microsoft Fabric**.  
It covers:

- Data ingestion  
- Data transformation  
- Dimensional data modeling  
- Orchestration and scheduling  
- SQL analytics  
- Power BI reporting  

The goal is to simulate a **real-world retail analytics workflow** using modern data engineering practices and Fabric Lakehouse architecture.

## 🚀 Technologies Used

- **Microsoft Fabric**
  - Lakehouse  
  - Notebooks (PySpark)  
  - SQL Endpoint  
  - Pipelines  
  - Dataflows Gen2  

- **Azure OneLake**

- **PySpark**

- **Delta Lake**

- **Power BI**

- **GitHub (Version Control)**

  ## 📂 Project Architecture

  <img width="1536" height="1024" alt="retail sales analytics diagram" src="https://github.com/user-attachments/assets/9470b9a4-0a10-479c-ade1-dade755cba2e" />


This architecture represents the full lifecycle of the data engineering workflow inside Microsoft Fabric — from raw data ingestion to analytics and reporting.

---

## 📊 Star Schema

The project uses a simple **dimensional model** to support analytics:

### **Dimension Tables**
- `dim_products`
- `dim_stores`

### **Fact Table**
- `fact_sales`  
  Contains aggregated metrics such as:
  - Quantity sold  
  - Sales amount  
  - Store and product references  

---

## 📡 Pipeline Workflow

### **1. Ingestion**
- Raw CSV files (`sales`, `products`, `stores`, `customers`) are uploaded into the **Fabric Lakehouse** under `/Files/raw/`.

---

### **2. Transformation (PySpark Notebooks)**
- Clean and standardize raw data  
- Apply schema validation  
- Convert to curated Delta tables  
- Prepare data for dimensional modeling  

---

### **3. Data Modeling**
- Build Star Schema:
  - `dim_products`
  - `dim_stores`
  - `fact_sales`

---

### **4. Data Quality Validation**
Validation includes:

- Row count comparisons  
- Null/blank checks  
- Foreign key integrity checks  
- Logging data quality issues into a monitoring table  

---

### **5. Scheduling**
- The entire pipeline is scheduled to run **daily at 6 AM IST** using Fabric Pipelines.

---

### **6. Visualization**
- A Power BI report is created using the **Lakehouse SQL Endpoint**  
- Includes KPIs, trends, product insights, and store performance  
- Supports interactive slicers for dynamic analysis  

---

If you want, I can now generate:

✅ Full README.md (all sections combined)  
✅ Pipeline JSON file  
✅ Notebook templates (PySpark)  
✅ Star Schema diagram PNG  
✅ GitHub portfolio formatting  

Just tell me!

