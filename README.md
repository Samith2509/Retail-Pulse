🛒 Retail Data Processing & Analytics Pipeline

An end-to-end Retail Data Engineering & Analytics project that simulates real-world retail data challenges such as dirty data ingestion, promotion analysis, loyalty point calculation, customer segmentation, and business insights using Python, Pandas, and SQL-style logic.

This project was designed in the context of a Retail Data Processing Hackathon and follows industry-style data layers and validation practices.

📌 Project Objectives

Simulate realistic retail datasets with intentional data quality issues

Build a robust ingestion & validation pipeline

Analyze promotion effectiveness

Implement a dynamic loyalty point calculation engine

Prepare the foundation for customer segmentation & engagement

🧠 High-Level Architecture
CSV Files (Raw Data)
        ↓
Raw Layer (No Validation)
        ↓
Data Quality Checks
        ↓
Staging (Clean Data)
        ↓
Analytics & Business Logic
        ↓
Insights (Promotions, Loyalty Points)

🗂️ Data Entities
1. Stores

store_id, store_name, store_city, store_region, opening_date

2. Products

product_id, product_name, product_category

unit_price, current_stock_level

3. Customers

customer_id, first_name, email

loyalty_status, total_loyalty_points

last_purchase_date, segment_id

4. Loyalty Rules

min_spend_threshold

points_per_unit_spend

bonus_points

5. Promotions

promotion_id, promotion_name

start_date, end_date

discount_percentage, applicable_category

6. Sales Data

Sales Header

transaction_id, customer_id, store_id

transaction_date, total_amount

Sales Line Items

line_item_id, transaction_id

product_id, promotion_id

quantity, line_item_amount

⚙️ Tech Stack

Python

Pandas & NumPy

Datetime utilities

CSV-based data lake simulation

SQL-style joins & aggregations using Pandas

🚀 Use Cases Implemented
✅ Use Case 1: Synthetic Data Generation with Quality Issues

What we do

Generate realistic retail datasets

Intentionally inject:

Duplicate IDs

Invalid foreign keys

Negative prices & quantities

Invalid dates

NULL values

Why

Mimics real production retail data

Enables meaningful data quality validation

Output

stores.csv

products.csv

customers.csv

loyalty_rules.csv

promotions.csv

sales_header.csv

sales_line_items.csv

✅ Use Case 2: Promotion Effectiveness Analyzer

Goal
Determine which promotions genuinely increase sales.

Steps

Load clean data from staging

Join:

Sales line items

Promotions

Products

Separate:

Promoted sales

Baseline (non-promoted) sales

Compute:

Sales lift (%)

Revenue lift (%)

Rank Top 3 most effective promotions

Key Metrics

Sales Lift % = (Promo Units - Baseline Units) / Baseline Units
Revenue Lift % = (Promo Revenue - Baseline Revenue) / Baseline Revenue


Why this approach

Transparent

Explainable

Business-friendly

No unnecessary ML complexity

✅ Use Case 3: Loyalty Point Calculation Engine

Goal
Automatically calculate loyalty points for every customer transaction.

Logic

Uses a rule-based system

Rules are driven by loyalty_rules table

Supports:

Minimum spend thresholds

Points per unit spend

Bonus points

Flow

Merge sales headers with customers

Apply loyalty rules dynamically

Calculate points per transaction

Aggregate points per customer

Update customer’s total loyalty balance

Why rule-based

Business rules change frequently

No code rewrite needed

Highly configurable

📊 Example Outputs

Promotion effectiveness table

Top 3 promotions by sales lift

Updated customer loyalty balances

📁 Project Structure
.
├── data_generation.py
├── promotion_effectiveness.py
├── loyalty_points_engine.py
├── stores.csv
├── products.csv
├── customers.csv
├── loyalty_rules.csv
├── promotions.csv
├── sales_header.csv
├── sales_line_items.csv
└── README.md

🔍 Key Design Decisions
Decision	Reason
Raw vs Staging layers	Enables auditing & debugging
Pandas over pure SQL	Faster prototyping & complex validation
Rule-driven loyalty logic	Business flexibility
No ML for promotions	Explainability & simplicity
🌱 Future Enhancements

Customer segmentation (RFM based)

Loyalty email notification system

Inventory vs sales correlation analysis

SQL / Cloud warehouse integration

Dashboard using Power BI / Tableau / Streamlit

🧾 How to Run
pip install pandas numpy
python data_generation.py
python promotion_effectiveness.py
python loyalty_points_engine.py

