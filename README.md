# E-commerce-SQL-Data-Analysis-Project
The objective of this project is to simulate how real-world data analysts in e-commerce and retail companies use SQL behind the scenes to:

✅ Build and structure a messy, real-world inventory database

✅ Perform Exploratory Data Analysis (EDA) to understand product categories, availability patterns, and pricing inconsistencies

✅ Clean and standardize raw data (handle nulls, remove invalid entries, convert pricing units)

✅ Write business-driven SQL queries to extract insights related to pricing, stock levels, revenue potential, and product performance

This project mirrors the actual workflow followed by analysts working in quick-commerce companies.

📁 Dataset Overview

The dataset was sourced from Kaggle and originally scraped from Zepto’s official product listings.

It closely resembles a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit).

⚠️ Duplicate product names exist intentionally — the same product may appear multiple times in different:

Package sizes

Weights

Discount variations

Categories

This reflects how real catalog data is structured in production systems.

🧾 Dataset Columns

sku_id – Synthetic primary key for each product

name – Product name as displayed on the app

category – Product category (Fruits, Snacks, Beverages, etc.)

mrp – Maximum Retail Price (originally stored in paise, converted to ₹)

discountPercent – Discount applied on MRP

discountedSellingPrice – Final selling price after discount (converted to ₹)

availableQuantity – Units available in inventory

weightInGms – Product weight in grams

outOfStock – Boolean indicator of stock availability

quantity – Units per package (may vary for loose produce vs packaged goods)

🔧 Project Workflow
1️⃣ Database & Table Creation

We begin by creating a structured SQL table with appropriate data types:

CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);

2️⃣ Data Import

The dataset was imported using pgAdmin’s import tool.

If import via UI is unavailable, the following command can be used:

\copy zepto(category,name,mrp,discountPercent,availableQuantity,
discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');

⚠️ Import Challenge

An encoding (UTF-8) error was encountered during import.

This was resolved by re-saving the CSV file in CSV UTF-8 format, ensuring compatibility with PostgreSQL.

🔍 3️⃣ Exploratory Data Analysis (EDA)

Initial exploration focused on understanding the structure and quality of the dataset:

Counted total number of records

Previewed sample rows

Checked for null values across all columns

Identified distinct product categories

Compared in-stock vs out-of-stock product counts

Detected duplicate product names representing multiple SKUs

This step helped uncover inconsistencies and prepared the dataset for cleaning.

🧹 4️⃣ Data Cleaning

To ensure accurate analysis, the following cleaning steps were performed:

Removed rows where MRP or discounted selling price was zero

Converted pricing columns from paise to rupees for readability and consistency

Verified discount calculations

Standardized numerical fields

This step ensures the data reflects realistic and usable pricing information.

📊 5️⃣ Business-Driven SQL Analysis

After cleaning, the focus shifted to generating meaningful business insights.

💰 Pricing & Discount Analysis

Identified top 10 products offering the highest discount percentage

Ranked top 5 categories by average discount

Flagged high-MRP products that are currently out of stock

📈 Revenue Estimation

Estimated potential revenue by category
(Selling Price × Available Quantity)

Identified categories contributing the highest inventory value

⚖️ Value-for-Money Analysis

Calculated price per gram to compare products fairly

Identified best value products across categories

📦 Inventory & Weight Analysis

Grouped products into Low, Medium, and Bulk weight segments

Measured total inventory weight per category

Analyzed stock distribution patterns
