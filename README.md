Customer Churn Analysis & Usage Patterns: End-to-End Data Pipeline
An end-to-end data analytics project exploring customer subscription churn and usage patterns. This repository covers data collection, cleaning, feature engineering in Python (Jupyter Notebook), database migration and querying in MySQL, and interactive dashboard creation in Power BI.


🚀 Project Workflow & Architecture
[Kaggle Dataset] 
       │
       ▼
[Python / Jupyter Notebook] ──(Data Cleaning & Feature Engineering)
       │
       ├────────────────────────► [Cleaned CSV Dataset]
       │
       ▼
[MySQL Database] ──────────────► (Advanced SQL Analysis & Churn Metrics)
       │
       ▼
[Power BI Dashboard] ──────────► (Interactive Visualizations & KPI Tracking)



🛠️ Tech Stack & Tools
Programming Language: Python 3.x
Libraries: Pandas, NumPy, SQLAlchemy, PyMySQL
Database: MySQL
BI Tool: Power BI Desktop
Development Environment: Jupyter Notebook, VS Code


📊 Step-by-Step Implementation Guide
Step 1: Data Collection & Extraction
Source: Downloaded raw customer data from Kaggle (customer_subscription_churn_usage_patterns.xlsx).
Initial Inspection: Loaded the dataset using Pandas and reviewed structural metrics (info(), describe(), head()).

Step 2: Data Cleaning & Preprocessing (Python / Jupyter Notebook)
The messy raw dataset underwent rigorous cleaning and validation:
Missing Value Imputation: Checked for nulls and filled missing numeric fields (e.g., Age, monthly_fee, tenure_months) using appropriate statistical measures (mean).
Duplicate Removal: Removed redundant records using drop_duplicates().
String Standardization: Cleaned categorical text columns (e.g., normalizing plan_type values like BASIC / PREMIUM into proper case format using .str.title()).

Outlier & Invalid Data Filtration:
Removed invalid rows where Age < 18 or Age >= 100.
Filtered out negative or corrupted financial entries (monthly_fee <= 0).
Date Parsing: Standardized signup_date to datetime objects.

Step 3: Feature Engineering
Created advanced analytical attributes to enrich the dataset for modeling and reporting:
Customer Lifetime Value (Customer_Value): Calculated as monthly_fee * tenure_months.
Tenure Cohorts (tenure_months): Segmented customers into bins (0-12 months, 13-24 months, 25-48 months, 49-72 months).
Senior Citizen Flag (Senior_Flag): Labeled customers as Senior (Age ≥ 60) or Adult (Age < 60).
Binary Churn Flag (Churn_Flag): Converted text churn labels (Yes/No) into binary integers (1/0).

Step 4: Exporting Cleaned Data to CSV
Exported the processed dataframe into a clean, structured flat file:

df.to_csv("Clean_Churn_Data.csv", index=False)
Step 5: Database Migration & SQL Analysis (MySQL)
Connected Jupyter Notebook to a local MySQL instance (churndb) using SQLAlchemy and PyMySQL.
Loaded the cleaned dataframe into a structured SQL table (customer_churn):

df.to_sql(name="customer_churn", con=engine, if_exists="replace", index=False)
Performed exploratory SQL queries to analyze churn rates across plan types, support ticket frequencies, and payment failure correlations.

Step 6: BI Dashboard Creation (Power BI)
Imported the cleaned dataset / connected directly to the MySQL database from Power BI.
Designed an interactive Customer Churn & Usage Patterns Dashboard featuring:

KPI Cards: Total Customers, Overall Churn Rate, Average Monthly Revenue, and Average Tenure.
Visual Breakdown: Churn distribution by plan type, weekly usage hours vs. churn likelihood, support ticket impact, and payment failure trends.


📁 Repository Structure
Plaintext
├── customer_subscription_churn_usage_patterns.xlsx   # Raw dataset from Kaggle
├── Clean_Churn_Data.csv                              # Cleaned dataset ready for BI/SQL
├── churn_analysis_notebook.ipynb                     # Jupyter notebook containing Python code
└── README.md                                         # Project documentatio


📌 Key Insights & Findings
Payment Failures: A strong correlation exists between payment failures and customer churn.
Engagement Thresholds: Users with lower average weekly usage hours are significantly more likely to churn.
Support Ticket Volume: Customers who submitted a higher number of support tickets without prompt resolution showed increased attrition rates.


👤 Author
Name: Subhanakr Panda
Computer Science Engineering (Data Science) Student

GitHub: 
