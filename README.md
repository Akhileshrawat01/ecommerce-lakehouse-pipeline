# E-Commerce Lakehouse ETL Pipeline (Medallion Architecture)
## Project Overview
This project implements an end-to-end Lakehouse ETL pipeline using PySpark and Delta Lake in Databricks with Unity Catalog enabled.

The pipeline processes multi-table e-commerce sales data and transforms raw CSV files into analytics-ready star schema tables using a Medallion Architecture (Bronze, Silver, Gold).

## Architecture
Raw CSV Files
→ Bronze Layer (Raw Delta Tables)
→ Silver Layer (Cleaned & Typed Data)
→ Gold Layer (Star Schema – Fact & Dimension Tables)

### Built using:
PySpark
Delta Lake
Unity Catalog
Partitioning & Z-Ordering
Incremental MERGE (Upsert logic)

### Platform:
Databricks

## Medallion Layers
### Bronze Layer (Raw Ingestion)
Explicit schema enforcement
CSV → Delta conversion
Raw data preserved without transformations
Tables:
orders_bronze
order_items_bronze
customers_bronze
products_bronze
payments_bronze

### Silver Layer (Data Cleaning & Standardization)
Timestamp casting
Date derivation (order_purchase_date)
Null handling
Duplicate removal
Numeric type enforcement

Tables:
orders_silver
order_items_silver
customers_silver
products_silver
payments_silver

### Gold Layer (Star Schema Modeling)
Fact Table
fact_sales

Grain: One row per order_id + product_id
Revenue = price + freight_value
Partitioned by order_purchase_date

Dimension Tables
dim_customer
dim_product
dim_date

