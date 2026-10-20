# Customer Shopping Behavior Analysis

## Overview
This project explores customer shopping behavior to understand purchasing patterns, product performance, discount usage, subscription status, and revenue trends. It uses Python for data preparation and exploratory data analysis (EDA), PostgreSQL for SQL-based analysis, and Power BI for interactive visualization.

> **Project scope:** The current files analyze customer shopping behavior, not customer churn. The project title is therefore based on the analyses present in the notebook, SQL file, and dashboard.

## Dataset
- **Dataset:** `customer_shopping_behavior.csv`
- **Main table:** `customer`
- **Fields used include:** customer ID, age, gender, category, item purchased, purchase amount, review rating, discount applied, shipping type, subscription status, previous purchases, and purchase frequency.
- The notebook also derives `age_group` and `purchase_frequency_days`.

The dataset is read from a local path in the notebook. Update that path to match where you save the CSV on your computer.

## Tools
- **Python:** Pandas and NumPy-style data preparation and EDA in Jupyter Notebook
- **PostgreSQL:** SQL queries for customer and sales analysis
- **SQLAlchemy / psycopg2:** Loading the prepared DataFrame into PostgreSQL
- **Power BI Desktop:** Dashboard and interactive filters
- **GitHub:** Project version control and documentation

## Steps
### 1. Load and explore the data
Load the CSV into a Pandas DataFrame. Inspect sample rows, column types, summary statistics, and missing values.

### 2. Clean and prepare the data
The notebook:
- Checks missing values and fills missing review ratings using the median review rating within each category.
- Standardizes column names to lowercase with underscores.
- Renames `purchase_amount_(usd)` to `purchase_amount`.
- Creates age groups using age quartiles.
- Converts purchase-frequency labels into an approximate number of days.
- Drops `promo_code_used` after checking it against `discount_applied`.

### 3. Load data into PostgreSQL
Use SQLAlchemy with the PostgreSQL driver to load the prepared DataFrame into a PostgreSQL table named `customer`. Configure your own local database connection details before running this step.

**Security note:** Do not commit database passwords or other credentials to GitHub. Replace hard-coded credentials with environment variables or another secure local configuration, and keep secrets out of the notebook.

### 4. Run PostgreSQL queries
The SQL file investigates:
- Revenue by gender
- Customers who used discounts but spent at least the average purchase amount
- Top five products by average review rating
- Average purchase amount for Standard and Express shipping
- Customer count, average spend, and total revenue by subscription status
- Products with the highest discount rates
- New, Returning, and Loyal customer segments
- Top three purchased products within each category
- Subscription status among repeat buyers
- Revenue contribution by age group

### 5. Build the Power BI dashboard
The supplied Power BI report includes visuals and filters for:
- Revenue by category
- Sales by category
- Revenue by age group
- Sales by age group
- Percentage of customers by subscription status
- Filters for gender, subscription status, category, and shipping type

Use the filters to explore how customer groups and shopping categories compare.

## Dashboard Results
The dashboard is designed to help explore:
- Which categories contribute more revenue and sales
- How revenue differs across age groups
- The distribution of customers by subscription status
- How gender, category, subscription status, and shipping type relate to the displayed metrics

Add specific numerical findings here after validating the dashboard results. No numerical conclusions are claimed in this README because they should be taken from the actual report and query outputs.

## How to Run
1. Download or place `customer_shopping_behavior.csv` in a folder on your computer.
2. Open `customer_shopping_analysis.ipynb` in Jupyter Notebook or JupyterLab.
3. Update the CSV file path in the first notebook cell, then run the notebook cells in order.
4. Install the required Python packages if needed:
   ```bash
   pip install pandas sqlalchemy psycopg2-binary jupyter
   ```
5. Create a PostgreSQL database (the notebook currently uses `customer_behaviour`) and securely configure your connection details.
6. Run the notebook cell that writes the cleaned DataFrame to the `customer` table.
7. Open `customer_shopping_analysis.sql` in pgAdmin or another PostgreSQL SQL client, connect to the correct database, and execute the queries.
8. Open `customer analysis.pbix` in Power BI Desktop and refresh the data connection if prompted. Update the source connection if your local setup differs.

## Repository Files
- `customer_shopping_analysis.ipynb` — data loading, exploration, cleaning, and PostgreSQL loading
- `customer_shopping_analysis.sql` — PostgreSQL analysis queries
- `customer analysis.pbix` — Power BI dashboard
- `customer_shopping_behavior.csv` — source dataset (add this file to the repository only if its licence and size permit)

## Key Takeaway
This project demonstrates an end-to-end analytics workflow: preparing customer data with Python, answering business questions with PostgreSQL, and communicating patterns through a Power BI dashboard.
