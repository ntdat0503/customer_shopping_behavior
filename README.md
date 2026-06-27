#  Customer Shopping Behavior 

A data analytics project analyzing customer shopping behavior using **Python**, **MySQL**, and **Power BI**.

---

##  Project Overview

This project explores a retail customer dataset to uncover insights about purchasing patterns, revenue trends, customer segmentation, and product performance. The analysis follows an industry-standard end-to-end workflow — from raw data to an interactive dashboard.

---

##  Repository Structure

```
customer-shopping-behavior/
│
├── data/
│   ├── customer_shopping_behavior.csv        # Raw dataset
│   └── customer_shopping_behavior_full.csv   # Cleaned & processed dataset
│
├── python/
│   └── Customer_shopping_behavior.ipynb      # Data cleaning & EDA notebook
│
├── sql/
│   └── project_customer_shopping_behavior.sql  # SQL analysis queries
│
├── dashboard/
│   └── customer_behavior_dashboard.png       # Screenshot of Power BI dashboard
│
└── README.md
```

---

##  Tools & Technologies

| Tool | Purpose |
|---|---|
| Python (Pandas) | Data cleaning, EDA, feature engineering |
| MySQL | Data storage & SQL analysis |
| Power BI | Interactive dashboard & visualization |
| GitHub | Version control & portfolio hosting |

---

##  Project Workflow

```
01 Business Problem Statement
        ↓ Import data into Python
02 Data Modelling & EDA in Python
        ↓ Load to SQL database
03 Data Analysis in SQL
        ↓ Connect with Power BI
04 Interactive Dashboard using Power BI
        ↓ Summarize findings
05 Project Report (this README)
```

---

##  Step 1 — Python: Data Cleaning & EDA

**File:** `python/Customer_shopping_behavior.ipynb`

Key steps performed:

- Loaded raw CSV and inspected dataset shape, dtypes, and summary statistics
- Handled missing values in `review_rating` by filling with **category-level median**
- Standardized column names (lowercase, underscores, renamed `purchase_amount_(usd)` → `purchase_amount`)
- Created new features:
  - `age_group` — segmented customers into 4 groups using `pd.qcut`: Young Adult, Adult, Middle-aged, Senior
  - `purchase_frequency_days` — mapped text frequency (Weekly, Monthly...) to numeric days
- Verified `discount_applied` and `promo_code_used` columns are identical
- Exported cleaned dataset as `customer_shopping_behavior_full.csv`

---

##  Step 2 — MySQL: Data Analysis

**File:** `sql/project_customer_shopping_behavior.sql`

### Business Questions Answered:

| # | Question |
|---|---|
| Q1 | Total revenue by gender |
| Q2 | Customers who used discount but spent above average |
| Q3 | Top 5 products by average review rating |
| Q4 | Average purchase amount: Standard vs Express shipping |
| Q5 | Do subscribed customers spend more? |
| Q6 | Top 5 products with highest discount rate |
| Q7 | Customer segmentation: New / Returning / Loyal |
| Q8 | Top 3 most purchased products per category |
| Q9 | Repeat buyers and their subscription likelihood |
| Q10 | Revenue contribution by age group |

### Key SQL Techniques Used:
- Aggregate functions (`SUM`, `AVG`, `COUNT`, `ROUND`)
- Subqueries
- `CASE WHEN` statements
---

##  Step 3 — Power BI: Interactive Dashboard

**File:** `dashboard/customer_behavior_dashboard.png`

### Dashboard Features:

**KPI Cards (top row):**
- Total Revenue: $233.08K
- Avg Purchase Amount: $59.76
- Total Customers: 3.90K
- Avg Rating: 3.75 / 5
- Subscription Revenue: $62.65K

**Visualizations:**
- Gender split (Donut chart)
- Customer count by age (Bar chart)
- Subscribed vs Non-subscribed customers (Pie chart)
- Sales & Revenue by Age group (Area + Bar chart)
- Sales & Revenue by Category (Area + Bar chart)
- Top 5 items by Revenue (Bar chart)
- Top 5 highest rated items (Table)

**Interactive Slicers:**
- Subscription status
- Gender
- Category
- Age group

---

##  Dataset Description

**Source:** Customer Shopping Behavior Dataset

| Column | Description |
|---|---|
| customer_id | Unique customer identifier |
| age | Customer age |
| gender | Male / Female |
| item_purchased | Product name |
| category | Product category (Clothing, Footwear, Accessories, Outerwear) |
| purchase_amount | Purchase value in USD |
| review_rating | Product rating (1–5) |
| subscription_status | Whether customer has subscription (Yes/No) |
| discount_applied | Whether discount was used (Yes/No) |
| previous_purchases | Number of past purchases |
| age_group | Derived: Young Adult / Adult / Middle-aged / Senior |
| purchase_frequency_days | Derived: Frequency in number of days |

---

##  Key Insights

- **Female customers** account for 68% of total customers and drive the majority of revenue
- **Young Adults** generate the highest revenue among all age groups
- **Clothing** is the top-selling category by both sales volume and revenue
- **Subscribed customers** contribute $62.65K — about 27% of total revenue
- **Blouse, Shirt, and Dress** are the top 3 revenue-generating products
- **Gloves** has the highest average review rating (3.86 / 5)

---

##  How to Run

### Python
```bash
pip install pandas jupyter
jupyter notebook python/Customer_shopping_behavior.ipynb
```

### MySQL
```sql
-- Create database and table, then import customer_shopping_behavior_full.csv
-- Run queries in sql/project_customer_shopping_behavior.sql
```

### Power BI
- Open Power BI Desktop
- Connect to MySQL database
- Load `customer_behavior` table
- Build visuals as described in dashboard section

---

## 👤 Author

> Built as part of an industry-standard End-to-End Data Analytics Portfolio project.
