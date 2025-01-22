
# Azure Car Sales Data Engineering Project

## Overview
The Azure Car Sales project demonstrates an end-to-end data engineering pipeline leveraging Azure cloud services. The pipeline extracts raw car sales data, processes it through multiple transformation layers (Bronze, Silver, and Gold), and visualizes insights using Power BI.

## Key Features
- **Data Sources:** Parquet files from Azure Data Lake Storage (ADLS).
- **Data Processing:** Incremental ETL using Azure Data Factory (ADF) and Databricks.
- **Data Storage:** Managed using Delta tables for the Gold layer.
- **Architecture Design:** Medallion architecture with Bronze, Silver, and Gold layers.
- **Data Governance:** Unity Catalog for schema management and access control.
- **Visualization:** Power BI dashboards showcasing processed data.

---

## Architecture
Below is the high-level architecture diagram of the pipeline:

![Azure_Sales_ETL_Architecture drawio](https://github.com/user-attachments/assets/eb4a84b2-ad0e-4be4-9a9c-d53ddc919aa1)

### Steps:
1. **Raw Data Ingestion (Bronze Layer):**
   - Raw data ingested into Azure Data Lake Storage (ADLS) from the provided [GitHub repository](https://github.com/SapnaSChavan/Azure_CarSales_Project/tree/main/RawData).

2. **Silver Layer Transformations:**
   - Data cleaning, derived column generation (e.g., `RevPerUnit`), and basic aggregations performed in Databricks.

3. **Gold Layer Transformations:**
   - Creation of dimension tables (`dim_branch`, `dim_date`, `dim_dealer`, `dim_model`) and a fact table (`factsales`).
   - Surrogate key generation and SCD Type-1 implementation for upserts.

4. **Data Visualization:**
   - Final insights visualized in Power BI dashboards connected to the Gold layer.

---

## Prerequisites
- **Azure Services:** Azure Data Lake Storage, Azure Data Factory, Azure Databricks.
- **Data Sources:** Parquet files stored in the Bronze layer.
- **Libraries:** PySpark, Delta Lake.
- **Tooling:** Power BI Desktop for visualization.

---

## Dataset Details
- **Raw Data:** Contains details of car sales including `Branch_ID`, `Dealer_ID`, `Model_ID`, `Date_ID`, `Revenue`, `Units_Sold`.
- **Derived Columns:**
  - `RevPerUnit`: Revenue per unit sold.
  - `Model_category`: Extracted from the `Model_ID` column.

---

## Implementation Steps
1. **Setup Azure Environment:**
   - Create ADLS containers for Bronze, Silver, and Gold layers.
   - Initialize Unity Catalog for schema management.
2. **Data Ingestion:**
   - Load raw data into the Bronze layer.
3. **Silver Layer Transformations:**
   - Use Databricks notebooks to perform cleaning and derive columns.
4. **Gold Layer Transformations:**
   - Implement dimension and fact tables with incremental data loading using Delta tables.
5. **Visualization:**
   - Connect Power BI to Gold layer tables for reporting and analysis.

---

## Repository Structure
```plaintext
├── RawData/                   # Source data files
├── notebooks/
│   ├── silver_notebook.py     # Silver layer transformations
│   ├── gold_dim_Branch.py     # Branch dimension table
│   ├── gold_dim_Date.py       # Date dimension table
│   ├── gold_dim_Dealer.py     # Dealer dimension table
│   ├── gold_dim_model.py      # Model dimension table
│   ├── gold_fact_sales.py     # Fact table creation
│   ├── db_notebook.py         # Database and catalog setup
├── README.md                  # Project documentation


## How to Run
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/SapnaSChavan/Azure_CarSales_Project.git
2. **Setup Azure Databricks Workspace:**
  Import notebooks into Databricks.
  Configure cluster with appropriate Spark configurations.
3. **Run Notebooks Sequentially:**
  Start with db_notebook.py to create the catalog and schemas.
  Execute Silver layer transformations.
  Proceed with Gold layer dimension and fact table creation.
4. **Connect Power BI:**
  Load Gold layer Delta tables for visualization.


This project is licensed under the MIT License. See the LICENSE file for details.

