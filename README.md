# customer_behavior_analysis
End-to-End Customer Behavior &amp; Purchase Patterns Analysis

##📌 Project Overview:
This project processes a dataset of 3,900 consumer records to isolate the operational drivers behind retail revenue. The pipeline cleanses unstructured consumer variables, engineers tracking metrics like age brackets and purchase intervals, structures a local relational database, and exposes data anomalies—such as a 100% operational correlation between promo code usage and discount distribution.


##🛠️ Tech Stack & ToolsData Processing: 
Python 3.x | Jupyter Notebook
Libraries: Pandas | SQLAlchemy | Psycopg2
Database Management: PostgreSQL
Business Intelligence: Power BI Desktop

##⚙️ Data Pipeline Architecture
###1.Data Cleaning & Feature Engineering (Python)
The source data underwent rigorous transformation stages inside Jupyter Notebook to ensure integrity before database ingestion:
-Imputation: Replaced 37 missing review_rating values by calculating group medians relative to each product category.
-Normalization: Standardised all schema headers to lowercase format and replaced spaces with underscores.
##Feature Engineering:
-Created age_group classifications: Young Adult (0-25), Adult (26-45), Middle-aged (46-60), and Senior (61+).
Converted categorical frequency intervals (frequency_of_purchases) into an exact numerical column purchase_frequency_days using custom mapping dictionaries (e.g., Weekly \(\rightarrow \) 7, Monthly \(\rightarrow \) 30).
-Redundancy Elimination: Validated that discount_applied matched promo_code_used across all 3,900 records, dropping the redundant promo_code_used column to save structural database storage.
##2. Database Storage & Structuring (PostgreSQL)
The engineered dataset was exported into a local PostgreSQL instance (customer_behaviour) using an SQLAlchemy engine link:
-Database Name: customer_behaviour
-Table Name: customer
-Schema Output: 19 optimized tracking columns tracking 3,900 active buyer profiles.3. 
##Visualisation Workflow (Power BI):
-Established a live database connection string targeting the local PostgreSQL instance.
-Modelled key metrics evaluating total capital volume (purchase_amount) against demographic slices.
