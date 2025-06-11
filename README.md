# Azure Databricks End-to-End Project

**Azure Databricks End-to-End Project**, designed specifically to build robust data engineering solutions for real-world business use cases.

---

## Project Overview

This project covers the entire data engineering lifecycle on Databricks with Azure Cloud, leveraging best practices and cutting-edge technologies. Such as:

- Build a **Medallion Architecture** with **Bronze, Silver, and Gold layers** to store raw, cleaned, and transformed data.
- Implement **incremental data loading** using **Spark Structured Streaming** and **Autoloader**, ensuring **exactly-once (idempotent)** data processing.
- Use **Delta Lake** formats and explore **Parquet** as the underlying file format.
- Master **PySpark programming** including UDFs, advanced PySpark functions, and Python OOP concepts like **classes** for reusable transformations.
- Gain expertise in **Unity Catalog** for data governance, security, and administrative tasks.
- Create detailed **data models** including **star schema** to represent fact and dimension tables.
- Build and implement **Slowly Changing Dimensions (SCD)** Type 1 and Type 2:
  - **SCD Type 1:** Update dimension records with new data (overwrite).
  - **SCD Type 2:** Maintain historical records using **Delta Live Tables (DLT)**, automating the process with simplified declarative APIs.
- Build and orchestrate **end-to-end ETL pipelines and workflows** within Databricks without relying on Azure Data Factory.
- Connect your data outputs with SQL Warehouses and external BI tools like **Power BI** through **Partner Connect** for seamless reporting.
- Learn to handle **real world constraints** such as schema evolution, security permissions, data contracts (expectations), and cluster management.

---

## Technologies & Services Used

- **Azure Databricks**
- **Azure Data Lake Storage (ADLS Gen2)**
- **Delta Lake**
- **Spark Structured Streaming & Autoloader**
- **Unity Catalog for governance & permissions**
- **Delta Live Tables for automated ETL & history tracking**
- **Azure SQL Warehouse / Databricks SQL Warehouse**
- **Power BI (via Partner Connect)**
- Python (PySpark with OOP)
- SQL within Databricks notebooks

---

## Architecture & Data Flow

1. **Bronze Layer**: Raw, incremental ingestion of data in Parquet format using Spark Autoloader streaming.
2. **Silver Layer**: Cleaned, enriched data stored in Delta format with transformations, PySpark functions, and application of Python classes for code modularity.
3. **Gold Layer**: Star schema with fact and dimension tables:
   - Dimensions using SCD Type 1 (manual coding) and SCD Type 2 using Delta Live Tables that automatically handle historical data.
   - Fact tables optimized with surrogate keys and relationships to dimensions.

Each layer is separated physically in different containers within ADLS connected to the Databricks workspace protected by Unity Catalog for security and governance. External locations and access connectors integrate storage securely.

---

## Stepwise Highlights

- **Account Setup & Storage Configuration**: Creating resource groups, storage accounts with hierarchical namespace enabled (for data lake capabilities), and containers for bronze, silver, and gold zones.
- **Unity Catalog Setup**: Managing meta stores, catalogs, external locations, credentials, and fine-tuned permission assignments.
- **Data Injection**: Using Databricks native no-code data injection tool to create managed Delta tables from external Parquet files.
- **Dynamic Streaming Notebooks**: Parameterized notebooks to perform incremental streaming loads for multiple datasets (orders, customers, products) using Autoloader and maintaining checkpoint and schema state for exactly-once processing.
- **Silver Layer Transformations**: Reusing functions, applying PySpark window functions (rank, dense_rank, row_number), applying OOP with Python classes for transformation reusability, and cleaning schema (dropping rescue columns).
- **Building and Governing Functions**: Creating reusable SQL scalar and Python functions within Unity Catalog for modular, production-ready code.
- **Gold Layer Implementation**:
   - Creating dimension schemas and star schema tables.
   - Creating surrogate keys with monotonically_increasing_id for join optimization.
   - Implementing SCD Type 1 (overwrite with upsert logic) and SCD Type 2 using Delta Live Tables (automated merge, history tracking).
   - Managing create_date and update_date to track changes accurately.
   - Implementing the upsert (merge) operations for fact and dimension tables using Delta Lake APIs.
- **Delta Live Tables (DLT)**: Declarative ETL pipelines to automate streaming ingestion, transformations, SCD handling, and data quality via expectations with warnings or failures.
- **Job Orchestration**: Building workflows and parent/child job pipelines with dependency management ensuring parallel execution where possible for efficiency.
- **SQL Warehouse & BI integration**: Create SQL warehouses with optimized cluster sizes, run SQL queries over Delta tables, save queries and build visualizations inside Databricks UI, or connect Power BI dashboards through Partner Connect.

---

## Project Directory Structure
```
/data-bricks-etl-project
├── notebooks/
│   ├── bronze_layer.ipynb          # Incremental streaming ingestion & autoloader
│   ├── silver_orders.ipynb         # Transformations & enrichments for orders
│   ├── silver_customers.ipynb      # Customer dimension preprocessing
│   ├── silver_products.ipynb       # Product transformations & UDFs
│   ├── gold_customers.ipynb        # SCD Type 1 handling & dimension loading
│   ├── gold_products.ipynb         # Delta Live Tables for SCD Type 2 dimension
│   ├── fact_orders.ipynb           # Fact table with surrogate keys & upsert
│   ├── parameters.ipynb            # Parameterization file for dynamic notebook execution
│   └── pipeline_orchestration.ipynb # Workflow orchestration and pipelines
├── datasets/                      # Raw/Parquet datasets splitted for incremental loading
├── docs/                          # Supporting documentation & diagrams
└── README.md                      # This file
```

---

## How to Run

1. **Set up Azure environment** using provided scripts/guidelines: resource groups, datalake, databricks workspace, and connectors.
2. **Upload Parquet files** into source container simulating incremental data arrival.
3. **Configure Unity Catalog**: Create meta stores, catalogs, schemas, external locations with proper permissions.
4. **Run notebooks in order**:
   - Bronze ingestion: run `bronze_layer.ipynb`
   - Silver transformations: run `silver_orders.ipynb`, `silver_customers.ipynb`, `silver_products.ipynb` in parallel
   - Gold layers: run dimension notebooks followed by fact table ingestion.
5. **Use workflows/job runs** to schedule and orchestrate all notebooks in production scenarios.
6. **Query Gold Layer** via SQL Warehouse or external BI tools (Power BI, Tableau).
7. **Monitor jobs and verify data quality** using Delta Lake logs and Delta Live Tables expectations.

---

## Additional Resources

- [Azure Databricks Documentation](https://docs.microsoft.com/en-us/azure/databricks/)
- [Delta Lake Documentation](https://docs.delta.io/latest/index.html)
- [Spark Structured Streaming Guide](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)
- [Unity Catalog Documentation](https://docs.databricks.com/data-governance/unity-catalog/index.html)
- [Delta Live Tables](https://docs.databricks.com/data-engineering/delta-live-tables/index.html)
- [Power BI Integration with Databricks](https://docs.microsoft.com/en-us/power-bi/connect-data/service-azure-databricks)
