# 🏬 Retail Data Processing & Analytics Pipeline  
**End-to-End Design & Implementation (6 Case Studies)**

---

## 📌 Project Overview

This project implements a realistic **retail data processing and analytics pipeline** using Python and Pandas.  
It demonstrates how real-world retail data problems are **designed, validated, and solved** using a structured, production-style approach.

The system simulates **dirty input data**, applies **data quality validation**, and builds **business analytics use cases** on top of trusted data.

---

## 🏗️ Overall Architecture

Raw CSV Data (Untrusted)
↓
Data Quality Validation
↓
Staging (Clean Data)
↓
Business Logic
↓
Analytics & Reports



### Design Principles
- Raw data is never trusted
- Invalid data is quarantined, not deleted
- Analytics use only validated data
- Each use case builds on clean staging data

---

## 📂 Data Sources

The pipeline processes the following datasets:
- Stores
- Products
- Customers
- Loyalty Rules
- Promotions
- Sales Header
- Sales Line Items

The raw data intentionally includes:
- Duplicate records
- Invalid foreign keys
- Negative values
- Invalid dates
- Broken business rules  

This ensures the pipeline is robust and production-ready.

---

##  Use Case 1: Automated Data Ingestion & Quality Validation Pipeline

###  Goal  
Ensure that **high-volume retail data** is ingested reliably and **validated for quality** before it is used for analytics or business decisions.

---

### 🔧 Approach  

#### Raw Data Ingestion
- Raw CSV files are generated and ingested for:
  - Stores  
  - Products  
  - Customers  
  - Sales headers  
  - Sales line items  
- Data is loaded into a **raw (untrusted) layer without modification** to preserve original records.

To simulate real-world retail environments, the raw data intentionally contains:
- Duplicate IDs  
- Invalid categories or store regions  
- Negative prices and quantities  
- Invalid transaction or reference IDs  

This mirrors **POS failures, upstream system issues, and manual data errors** commonly seen in enterprise systems.

---

#### Schema & Referential Validation
- Verify mandatory fields such as:
  - `store_id`, `product_id`, `transaction_id`
- Enforce foreign key relationships:
  - `product_id` in sales must exist in the products dataset
  - `store_id` in sales must exist in the stores dataset

---

#### Entity-Specific Business Rule Validation

**Stores**
- Duplicate `store_id`
- Missing `store_name`
- Invalid `store_region`
- Invalid `opening_date`

**Products**
- Duplicate `product_id`
- Invalid product category
- Negative price or stock quantity

**Customers**
- Duplicate customer ID or email
- Negative loyalty points
- Invalid last purchase date

**Sales**
- Invalid store or product references
- Negative transaction amounts
- Invalid quantities

These checks ensure both **technical correctness and business consistency**.

---

#### Staging & Quarantine Design
- ✅ **Valid records** → `staging_*.csv` (Clean Layer)  
- ❌ **Invalid records** → `quarantine_*.csv`  

Each rejected record includes:
- `error_reason`
- Original data values for full traceability

This design guarantees **auditability, transparency, and compliance**, which are critical in enterprise data pipelines.

---

###  Outcome
- Only **clean, trusted data** flows into downstream analytics and reporting
- Invalid data is **quarantined, not deleted**, enabling audits and root-cause analysis
- Establishes a strong **data quality foundation** for all subsequent use cases


## Use Case 2: Real-Time Promotion Effectiveness Analyzer

### Goal
Identify which promotions actually drive sales and revenue growth.

### Approach

#### Data Joining
- Join clean sales line items with promotion details and product information.

#### Baseline vs Promoted Comparison
Compare sales volume and revenue:
- When a product is sold under a promotion
- Versus when it is sold without a promotion

#### Effectiveness Metrics
Calculate:
- Sales uplift percentage
- Revenue growth per promotion
- Performance by product category

#### Ranking & Reporting
- Rank promotions by effectiveness.
- Highlight **Top 3 promotions** that drive the highest sales uplift.

### Outcome
- Business teams can stop ineffective promotions.
- Increased investment in high-impact promotions.

---

## Use Case 3: Loyalty Point Calculation Engine

### Goal
Accurately calculate and accrue loyalty points for customers after each transaction.

### Approach

#### Transaction Identification
- Identify completed sales transactions from clean sales header data.

#### Customer & Rule Mapping
- Join transactions with customer details.
- Apply relevant loyalty rules based on spend amount, date, or special conditions.

#### Points Calculation
- Calculate base points (e.g., points per currency unit spent).
- Apply bonus points for qualifying transactions (high spend, weekends, etc.).

#### Balance Update
- Add newly earned points to the customer’s total loyalty balance.

### Outcome
- Loyalty points are calculated consistently and transparently.
- Customers are rewarded accurately, improving trust and retention.

---

## Use Case 4: Customer Segmentation for Targeted Offers

### Goal
Identify high-value and at-risk customers for personalized marketing.

### Approach

#### Sales Aggregation
- Aggregate customer sales history from clean sales data.

#### RFM Analysis
Calculate:
- **Recency**: How recently the customer purchased
- **Frequency**: How often the customer purchases
- **Monetary**: How much the customer spends

#### Loyalty Signal Integration
- Include current loyalty point balance as an additional indicator of engagement.

#### Segment Creation
- **High-Spenders**: Top customers by monetary value
- **At-Risk Customers**: No recent purchases but still holding loyalty points

### Outcome
- Enables targeted marketing campaigns.
- Higher conversion rates and reduced churn.

---

## Use Case 5: Automated Loyalty Notification System

### Goal
Close the loyalty loop by informing customers about earned rewards.

### Approach

#### Trigger Identification
- Detect customers whose loyalty points were updated in the latest run.

#### Customer Communication Mapping
- Retrieve customer email and loyalty details.

#### Personalized Messageity Message Creation
- Generate dynamic messages including:
  - Points earned in the transaction
  - Total loyalty balance
  - Encouragement to shop again

#### Notification Simulation
- Simulate email delivery (or integrate with real email services in production systems).

### Outcome
- Customers feel acknowledged and rewarded.
- Increased engagement and repeat purchases.

---

## Use Case 6: Inventory & Store Performance Correlation

### Goal
Understand how inventory availability affects sales performance.

### Approach

#### Inventory & Sales Integration
- Join sales data with daily inventory levels by store and product.

#### Top Product Identification
- Identify the top-selling products across all stores.

#### Out-of-Stock Analysis
- Calculate how often these products were unavailable.
- Measure lost sales opportunities due to stock-outs.

#### Business Insight Generation
- Estimate potential revenue lost because of inventory shortages.

### Outcome
- Data-driven inventory planning.
- Reduced stock-outs and improved store performance.

---

## 🛠️ Technologies Used
- Python
- Pandas & NumPy
- CSV-based data pipeline
- Rule-based validation
- Analytical aggregations

---

## 🎯 Why This Design Works
- Mimics real enterprise data pipelines
- Clean separation of data layers
- Fully auditable data quality handling
- Scalable and extensible architecture

---

## 🚀 Future Enhancements
- Replace CSV with databases
- Add real-time streaming
- Automate alerts and dashboards
- Convert logic to SQL or Spark

---
