# Ecommerce Sales ETL Project

This project demonstrates an end-to-end ETL (Extract, Transform, Load) pipeline for an ecommerce sales dataset using PySpark and Delta Lake on Databricks. The workflow covers data ingestion, cleaning, transformation, and analytics, following the medallion architecture (Bronze, Silver, Gold layers). The project culminates with a Power BI dashboard for business intelligence and data visualization.

## Project Structure

- **Bronze Layer:** Raw data ingestion from CSV files into Delta tables.
- **Silver Layer:** Data cleaning, joining, and enrichment to create analytics-ready tables.
- **Gold Layer:** Aggregated and business-focused tables for reporting and advanced analytics.
- **Power BI Dashboard:** Interactive visualizations and business intelligence reports.

## Data Sources

The project uses the Olist ecommerce dataset, with the following files:
- `olist_customers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_translation.csv`

All files are expected in `/FileStore/tables/olist/` on Databricks.

## Main Steps

### 1. Data Ingestion
Load each CSV file into a Delta table with an explicit schema using PySpark's structured data types.

### 2. Data Cleaning
- Remove duplicate files and validate data integrity
- Handle missing values and data quality issues
- Standardize data formats and types

### 3. Bronze Layer
Save raw ingested data as Delta tables in `/mnt/olist/bronze/` with the following tables:
- `customers`
- `geolocation`
- `order_items`
- `order_payments` (payments)
- `order_reviews` (reviews)
- `orders`
- `products`
- `sellers`
- `product_category_map` (translation)

### 4. Silver Layer
- **Data Integration:** Join datasets to create a unified view (`orders_customers_category`)
- **Exploratory Data Analysis (EDA):**
  - Missing values analysis
  - Statistical summaries
  - Customer and order behavior patterns
  - Time-based analysis
  - Shipping and logistics metrics
  - Revenue analysis
- **Intermediate Analytics Tables:**
  - `orders_per_customer`
  - `items_per_order`
  - `top_sales`
  - `top_categories`
  - `month_orders`
  - `avg_delivery_day`
  - `delivery_time_state`

### 5. Gold Layer
Create business-focused aggregations and register as Delta tables in the `gold` schema:
- **`monthly_state_revenue`:** Revenue trends by state and month
- **`top_10_categories`:** Top performing product categories by revenue
- **`customer_lifetime_value`:** Customer lifetime value analysis
- **`repeat_customers`:** Customer retention and repeat purchase analysis
- **`delivery_time_by_category`:** Average delivery times by product category

### 6. Power BI Integration
- Connect Power BI to Databricks Delta tables in the `gold` schema
- Create interactive dashboards featuring:
  - Revenue trends and KPIs
  - Geographic sales distribution
  - Product category performance
  - Customer behavior insights
  - Delivery performance metrics
  - Time-series analysis

## Key Analytics and Insights

The pipeline generates insights across multiple business dimensions:

- **Sales Performance:** Revenue by state, category, and time periods
- **Customer Analytics:** Lifetime value, repeat purchase behavior, geographic distribution
- **Product Analytics:** Top-selling products and categories, pricing analysis
- **Logistics:** Delivery time analysis, shipping performance by region
- **Temporal Trends:** Monthly and seasonal sales patterns

## Architecture Highlights

- **Medallion Architecture:** Bronze → Silver → Gold layer progression ensures data quality and governance
- **Delta Lake:** Provides ACID transactions, versioning, and efficient querying
- **Schema Evolution:** Explicit schema definitions ensure data consistency
- **Modular Design:** Structured approach allows for easy maintenance and extension
- **BI Integration:** Seamless connection to Power BI for business user consumption

## How to Run

1. **Data Setup:**
   - Upload the dataset files to `/FileStore/tables/olist/` in your Databricks workspace

2. **ETL Pipeline:**
   - Open and run the notebook: [`Ecommerce Sales ETL Project.ipynb`](Ecommerce%20Sales%20ETL%20Project.ipynb)
   - The notebook will create Delta tables in all three layers

3. **Power BI Dashboard:**
   - Connect Power BI to your Databricks workspace
   - Import tables from the `gold` schema
   - Create visualizations using the pre-aggregated gold layer tables

## Requirements

- **Platform:** Databricks workspace (or compatible Spark environment)
- **Technologies:** PySpark, Delta Lake
- **Visualization:** Power BI Desktop/Service
- **Storage:** Databricks File System (DBFS) with mounted storage

## Outputs

### Data Assets
- Cleaned and joined datasets for analytics
- Aggregated tables optimized for business insights
- Registered Delta tables in Databricks metastore

### Business Intelligence
- Interactive Power BI dashboard
- Self-service analytics capabilities
- Real-time data refresh from Delta tables



**Dataset Source:**  
[Olist Brazilian Ecommerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

**Technologies Used:**  
Databricks | PySpark | Delta Lake | Power BI | Python
