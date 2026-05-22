# Customer Shopping Behavior Analysis

An end-to-end data analytics project exploring consumer purchasing patterns, demographic distributions, and transaction insights using **Python**, **PostgreSQL**, and **Power BI**.

---

## 📌 Project Overview
This project processes a retail dataset of 3,900 consumer records to isolate the operational drivers behind revenue. The pipeline cleanses unstructured consumer variables, imputes missing review indicators, engineers new tracking features (age groups and purchase intervals), structures a relational database, and exposes data redundancies to optimize database storage.

---

## 🛠️ Tech Stack & Tools
* **Data Processing**: Python 3.x | Jupyter Notebook
* **Libraries**: Pandas | SQLAlchemy | Psycopg2
* **Database Management**: PostgreSQL
* **Business Intelligence**: Power BI Desktop

---

## ⚙️ Data Pipeline Architecture

### 1. Data Cleaning & Feature Engineering (Python)
The source data underwent transformation stages inside Jupyter Notebook to ensure integrity before database ingestion:
* **Imputation**: Identified 37 missing values in `review_rating`. Replaced them by calculating the median rating relative to each product `category`.
* **Normalization**: Standardised all schema headers to lowercase format and replaced spaces with underscores for SQL compatibility.
* **Feature Engineering**: 
  * Created `age_group` classifications: *Young Adult (0-25)*, *Adult (26-45)*, *Middle-aged (46-60)*, and *Senior (61+)* using `pd.cut`.
  * Mapped categorical frequency intervals (`frequency_of_purchases`) into an exact numerical column `purchase_frequency_days` (e.g., Weekly \(\rightarrow\) 7, Monthly \(\rightarrow\) 30).
* **Redundancy Elimination**: Validated that `discount_applied` perfectly matched `promo_code_used` across all 3,900 records, dropping the redundant `promo_code_used` column.

### 2. Database Storage & Ingestion (PostgreSQL)
The engineered dataset was exported into a local PostgreSQL instance using an SQLAlchemy engine link:
* **Database Name**: `customer_behaviour`
* **Table Name**: `customer`
* **Schema Output**: 19 optimized tracking columns tracking 3,900 active buyer profiles.

### 3. Visualisation Workflow (Power BI)
* Established a database connection string targeting the local PostgreSQL instance.
* Modelled key metrics evaluating total capital volume (`purchase_amount`) against demographic slices.

---

## 📦 Repository Structure
```text
├── data/
│   └── customer_shopping_behavior.csv     # Raw source dataset
├── notebooks/
│   └── data_cleaning_pipeline.ipynb       # Python cleaning and feature engineering
├── sql/
│   └── queries.sql                        # SQL verification queries
├── dashboard/
│   └── customer_analysis_report.pbip      # Power BI project folder/file
└── README.md                              # Project documentation
```

---

## 🚀 Step-by-Step Implementation Guide

### Step 1: Clone the Project
```bash
git clone https://github.com
cd customer_behavior_analysis
```

### Step 2: Run the Processing Notebook
Ensure you have your environment libraries installed (`pandas`, `sqlalchemy`, `psycopg2`). Open the Jupyter Notebook file to execute the pipeline:
```python
# Key Python Pipeline Snip
df['review_rating'] = df.groupby('category')['review_rating'].transform(lambda x: x.fillna(x.median()))
df['age_group'] = pd.cut(df['age'], bins=[0,25,45,60,150], labels=['Young Adult', 'Adult', 'Middle-aged', 'Senior'])

# Ingestion to PostgreSQL
engine = create_engine("postgresql+psycopg2://postgres:121976@localhost:5432/customer_behaviour")
df.to_sql("customer", engine, if_exists='replace', index=False)
```

### Step 3: Database Verification (PostgreSQL)
Log into your local PostgreSQL console to verify table migration performance:
```sql
-- Verify total rows uploaded
SELECT COUNT(*) FROM customer; 

-- View average spending across age brackets
SELECT age_group, AVG(purchase_amount) AS avg_spent 
FROM customer 
GROUP BY age_group;
```

---



## 📊 Dashboard Showcase

Below is a comprehensive walkthrough demonstrating the interactive features, demographic filters, and visual KPIs built into the Power BI dashboard:

👉 [**Watch the Live Dashboard Demo on Google Drive**](https://drive.google.com/file/d/1mgjA1-65gLRrWa7dRq_0kIMdrl7_zrjU/view?usp=sharing)





* **Demographic Slicing**: Evaluates spending distribution behaviors across defined age groups and gender categories.
* **Operational Tractions**: Pinpoints category-specific revenue performance alongside target purchase frequencies.
