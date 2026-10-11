# Customer Subscription Churn & Usage Patterns: End-to-End Data Pipeline

An end-to-end data analytics project exploring customer subscription churn and usage patterns. This repository covers data collection from Kaggle, messy data cleaning and feature engineering in Python (Jupyter Notebook), database migration and querying in MySQL, and an interactive dashboard built in Power BI.

---

## 🚀 Project Architecture & Workflow

```
[Kaggle Dataset (.xlsx)] 
       │
       ▼
[Python / Jupyter Notebook] ──(Data Cleaning & Feature Engineering)
       │
       ├────────────────────────► [Cleaned Dataset (.csv)]
       │
       ▼
[MySQL Database (`churndb`)] ──► (Database Storage & Structured Queries)
       │
       ▼
[Power BI Dashboard (.pbix)] ──► (Interactive Visualizations & KPIs)
```

---

## 🛠️ Tech Stack & Tools

* **Programming Language:** Python
* **Libraries:** Pandas, NumPy, SQLAlchemy, PyMySQL
* **Database Management:** MySQL (via MySQL Workbench / PyMySQL engine)
* **BI & Visualization:** Power BI Desktop
* **Environment:** Jupyter Notebook

---

## 📋 Step-by-Step Implementation Guide

### 1. Data Collection & Extraction
* **Source:** Acquired raw subscriber usage and churn data from Kaggle (`customer_subscription_churn_usage_patterns.xlsx`).
* **Initial Inspection:** Loaded the Excel file into a Pandas DataFrame to analyze data types, missing values, and structure (`df.info()`, `df.describe()`).

### 2. Data Cleaning & Preprocessing (Python)
Performed rigorous data hygiene steps in Jupyter Notebook:
* **Null Value Handling:** Inspected missing value counts and imputed numeric columns (`Age`, `monthly_fee`, `tenure_months`) using statistical averages (mean).
* **Duplicate Elimination:** Checked and removed duplicate records using `df.drop_duplicates()`.
* **String Standardization:** Trimmed whitespaces and standardized categorical text columns (e.g., proper-casing `plan_type` values like `BASIC`, `premium`, `STANDARD` into uniform title case).
* **Outlier Filtration:** 
  * Filtered out invalid age demographics (`Age < 18` or `Age >= 100`).
  * Removed corrupted or negative pricing entries (`monthly_fee <= 0`).
* **Datetime Formatting:** Converted `signup_date` strings into standard datetime objects.

### 3. Feature Engineering
Enriched the dataset by engineering high-value analytical features:
* **Customer Lifetime Value (`Customer_Value`):** Calculated dynamically as `monthly_fee * tenure_months`.
* **Tenure Cohorts (`tenure_months`):** Segmented tenure lengths into intuitive operational bins (`0-12 months`, `13-24 months`, `25-48 months`, `49-72 months`).
* **Senior Citizen Flag (`Senior_Flag`):** Categorized users into `Senior` (Age ≥ 60) and `Adult` (Age < 60) flags.
* **Binary Churn Flag (`Churn_Flag`):** Converted text status (`Yes`/`No`) into binary integers (`1`/`0`) for easier aggregation and modeling.

### 4. Exporting Cleaned Data
* Exported the final processed dataframe into a clean flat file for downstream tools:
  ```python
  df.to_csv("Clean_Churn_Data.csv", index=False)
  ```

### 5. Database Migration & SQL Analysis (MySQL)
* Established a secure connection to a local MySQL database (`churndb`) using SQLAlchemy and PyMySQL.
* Migrated the cleaned dataframe directly into a relational SQL table (`customer_churn`):
  ```python
  df.to_sql(name="customer_churn", con=engine, if_exists="replace", index=False)
  ```
* Ran structured SQL queries to analyze subscription tier drop-offs, billing failure frequencies, and customer support ticket trends.

### 6. BI Dashboard Creation (Power BI)
* Connected Power BI to the processed dataset / SQL database.
* Developed an interactive **Customer Churn & Usage Patterns Dashboard** (`Churn_Analysis_Dashboard.pbix`) featuring:
  * **Summary KPI Cards:** Total Customers, Active vs. Churned Users, Overall Churn Rate, and Average Monthly Revenue.
  * **Deep-Dive Visuals:** Churn breakdown by subscription plan type, average weekly usage hours against attrition risk, payment failure correlations, and support ticket escalation impacts.

---

## 📁 Repository Structure

```text
├── customer_subscription_churn_usage_patterns.xlsx   # Raw Kaggle dataset
├── Clean_Churn_Data.csv                              # Processed clean dataset ready for BI/SQL
├── Churn DataSet Cleaning.ipynb                      # Jupyter Notebook containing end-to-end Python code
├── Churn_Analysis_Dashboard.pbix                     # Power BI interactive dashboard file
└── README.md                                         # Project documentation
```

---

## 💡 Key Analytical Findings
* **Payment Reliability:** Payment failures display a high positive correlation with customer churn likelihood.
* **Engagement Drop-offs:** Subscribers with lower average weekly usage hours are significantly more prone to terminating their subscriptions.
* **Support Friction:** High volumes of unresolved support tickets heavily accelerate user attrition across all subscription tiers.

---

## 👤 Author
* **Role:** Data Science & Analytics Student
* **GitHub Profile:** [Your GitHub Profile Link](https://github.com/your-username)