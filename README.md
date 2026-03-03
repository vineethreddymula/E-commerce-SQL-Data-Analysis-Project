# E-commerce-SQL-Data-Analysis-Project
In this project, I built and analyzed a real-world e-commerce inventory database using SQL.

I structured raw catalog data into table, performed exploratory data analysis (EDA), cleaned pricing and inventory inconsistencies, and standardized the dataset for accurate analysis.

Using business-driven SQL queries, I generated insights on discounts, pricing patterns, stock availability, revenue potential, and value-for-money comparisons.

This project replicates the practical workflow followed by data analysts in quick-commerce and retail companies.
The goal is to transform raw, messy catalog data into structured, business-ready insights using SQL.

Through this project, we:

✅ Build and structure a real-world inventory database

✅ Perform Exploratory Data Analysis (EDA)

✅ Clean and standardize raw product data

✅ Generate business-driven insights using SQL queries

This mirrors how analysts work behind the scenes in retail, marketplace, and quick-commerce platforms.

📁 Dataset Overview

The dataset was sourced from Kaggle and originally scraped from Zepto’s official product listings.

It represents a realistic e-commerce inventory system where:

Each row corresponds to a unique SKU (Stock Keeping Unit)

Duplicate product names intentionally exist

The same product may appear in different:

Package sizes

Weights

Discount variations

Categories

This reflects how real production catalog systems store data.

🧾 Dataset Columns
Column Name	Description
sku_id	Synthetic primary key for each product
name	Product name as displayed in the app
category	Product category (Fruits, Snacks, Beverages, etc.)
mrp	Maximum Retail Price (converted from paise to ₹)
discountPercent	Discount applied on MRP
discountedSellingPrice	Final selling price after discount (₹)
availableQuantity	Units available in inventory
weightInGms	Product weight in grams
outOfStock	Boolean indicator of stock availability
quantity	Units per package
🏗️ 1️⃣ Database & Table Creation

A structured PostgreSQL table was created with appropriate data types:

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

📥 2️⃣ Data Import

The dataset was imported using pgAdmin’s import tool.

Alternatively, the following command can be used:

\copy zepto(category,name,mrp,discountPercent,availableQuantity,
discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (
    FORMAT csv,
    HEADER true,
    DELIMITER ',',
    QUOTE '"',
    ENCODING 'UTF8'
);

⚠️ Import Issue & Resolution

An encoding (UTF-8) error occurred during import.

This was resolved by re-saving the CSV file in CSV UTF-8 format, ensuring compatibility with PostgreSQL.

🔍 3️⃣ Exploratory Data Analysis (EDA)

Initial exploration focused on understanding structure, quality, and data distribution.

Key steps included:

Counting total records

Previewing sample rows

Checking null values across all columns

Identifying distinct product categories

Comparing in-stock vs out-of-stock products

Detecting duplicate product names representing multiple SKUs

This phase helped uncover inconsistencies and prepare the dataset for cleaning.

🧹 4️⃣ Data Cleaning & Standardization

To ensure analytical accuracy:

Removed rows where mrp or discountedSellingPrice was zero

Converted pricing columns from paise to rupees

Verified discount percentage calculations

Standardized numeric fields

Ensured boolean values were correctly formatted

After cleaning, the dataset reflected realistic pricing and inventory information.

📊 5️⃣ Business-Driven SQL Analysis

With clean data, SQL was used to extract actionable business insights.

💰 Pricing & Discount Analysis

Top 10 products offering the highest discount percentage

Top 5 categories ranked by average discount

High-MRP products currently out of stock

📈 Revenue Estimation

Estimated potential revenue per category

Revenue = discountedSellingPrice × availableQuantity


Identified categories contributing the highest inventory value

⚖️ Value-for-Money Analysis

Calculated price per gram for fair product comparison

Identified best-value products across categories

📦 Inventory & Weight Analysis

Segmented products into:

Low weight

Medium weight

Bulk weight

Measured total inventory weight per category

Analyzed stock distribution patterns.

This project demonstrates how raw, messy e-commerce data can be transformed into structured, business-ready insights using SQL. From database design and data cleaning to analytical querying, it reflects the real-world workflow of data analysts in retail and quick-commerce environments.
