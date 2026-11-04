# Velora – Customer Shopping Behaviour Analysis

An end-to-end retail analytics project exploring customer purchase patterns, product preferences, subscription behaviour and spending across Velora, a fashion retail brand. The project uses **Python, PostgreSQL, SQL and Power BI** to prepare customer data, answer business questions and present findings through an interactive dashboard.

## Project Objective

Velora wants to better understand what influences customer purchasing and repeat buying. This analysis examines customer demographics, product categories, subscription status, discounts, review ratings and shipping preferences to support marketing, sales and product decisions.

Key business questions include:

- Which product categories contribute the most to purchase value and sales volume?
- How do purchase patterns differ across age groups and genders?
- Do subscribers spend more than non-subscribers?
- Which products receive the highest review ratings?
- How are customers distributed across New, Returning and Loyal segments?
- How do discounts and shipping types relate to purchase behaviour?

## Dataset

The project uses a customer shopping behaviour dataset containing **3,900 records and 18 original columns**.

| Data area | Example fields |
|---|---|
| Customer demographics | Age, Gender, Location |
| Purchase details | Item Purchased, Category, Purchase Amount, Season, Size, Color |
| Customer behaviour | Subscription Status, Previous Purchases, Frequency of Purchases |
| Purchase preferences | Shipping Type, Discount Applied, Promo Code Used, Payment Method |
| Customer feedback | Review Rating |

The dataset is a static historical snapshot, not a live data feed. Each row represents one customer record in the supplied dataset; repeat-purchase behaviour is analyzed using the `Previous Purchases` field.

## Tools & Technologies

- **Python (Pandas)** – Data exploration, cleaning and feature engineering
- **PostgreSQL** – Storage of the prepared dataset
- **SQL** – Business analysis using aggregations, subqueries, CTEs and window functions
- **Power BI** – Data visualization and interactive dashboard development
- **Jupyter Notebook** – Python workflow documentation

## Project Workflow

### 1. Data Cleaning & Preparation – Python

The raw dataset was explored and prepared using Pandas.

Key steps:
- Reviewed dataset structure, data types, summary statistics and missing values.
- Handled **37 missing values** in `Review Rating` by imputing the median rating within each product category.
- Standardized column names to `snake_case` for consistency and easier SQL use.
- Created an `age_group` feature using quartile-based age groups: Young Adult, Adult, Middle-aged and Senior.
- Converted purchase frequency categories into an approximate numeric `purchase_frequency_days` field.
- Checked `promo_code_used` against `discount_applied`; as the fields contained the same information, the redundant `promo_code_used` column was removed.
- Loaded the cleaned DataFrame into PostgreSQL using SQLAlchemy.

### 2. Data Analysis – PostgreSQL & SQL

SQL queries were written to answer the business questions in the requirements document.

Analysis includes:
- Revenue comparison by gender.
- Customers who used discounts but spent above the average purchase amount.
- Top five products by average review rating.
- Average purchase amount comparison between Standard and Express shipping.
- Subscriber versus non-subscriber customer count, average spend and total purchase value.
- Products with the highest percentage of discounted purchases.
- Customer segmentation into New, Returning and Loyal groups.
- Top three most purchased products within each category.
- Subscription distribution among repeat buyers with more than five previous purchases.
- Purchase value contribution by age group.

SQL techniques used include `GROUP BY`, aggregate functions, filtering, subqueries, `CASE` statements, Common Table Expressions (CTEs), and window functions such as `DENSE_RANK()`.

**Customer segment definitions used in the SQL analysis:**
- New: 1 or fewer previous purchases
- Returning: 2–10 previous purchases
- Loyal: More than 10 previous purchases

### 3. Dashboard Development – Power BI

The **Velora Customer Behaviour Dashboard** provides an interactive summary of customer and category performance.

Dashboard KPIs:
- Total Customers
- Average Purchase Amount
- Average Review Rating

Visualizations:
- Customer distribution by subscription status.
- Revenue by product category.
- Sales by product category.
- Purchase amount by age group.
- Sales by age group.

Interactive filters:
- Subscription Status
- Gender
- Product Category
- Shipping Type

### Dashboard Preview

<img width="893" height="497" alt="Screenshot 2026-10-27 153345" src="https://github.com/user-attachments/assets/0c542e50-cc46-4e94-a2a0-3f70438d92bf" />


## Key Findings

- **Purchase value is broadly consistent across segments:** The overall average purchase amount is **$59.76**. Average spending across the analyzed gender, age, subscription, discount and shipping groups varies by no more than approximately $2.30.
- **Clothing and Accessories lead category performance:** Together, these categories contribute approximately **76.6% of total purchase value**.
- **Subscription adoption is limited:** Approximately **27% of customers are subscribed**. Subscribers and non-subscribers have similar average purchase amounts (**$59.49 vs. $59.87**).
- **The customer base is largely established:** The report classifies **79.9%** of customers as Loyal, 18.0% as Returning and 2.1% as New, based on previous purchase counts.
- **Discounts do not show a clear increase in average spend:** Discounted purchases average **$59.28**, compared with **$60.13** for purchases without discounts.
- **Age-group spending differences are modest:** Young Adults contribute the largest share of purchase value, but the report notes that this is mainly related to group size.

## Business Recommendations

- Investigate the low subscription share and confirm why no female customers in this dataset are subscribed before designing targeted subscription campaigns.
- Develop loyalty initiatives that encourage repeat purchases and subscription adoption.
- Review blanket discounting and test targeted offers while monitoring sales and margins.
- Prioritize high-volume categories such as Clothing and Accessories, and use best-selling and highly rated products in merchandising campaigns.
- Treat age and shipping differences as modest signals rather than strong evidence for major targeting or pricing changes.

## Limitations & Data Notes

- The dataset is a static snapshot and does not represent a live retail system.
- Each row represents one customer record; repeat behaviour is inferred from `Previous Purchases`, not tracked through a sequence of dated transactions.
- The 37 missing review ratings were imputed using category-level medians.
- Subscription status is used as a proxy for customer loyalty; it is not a direct measure of retention.
- No female subscribers appear in the dataset, so gender and subscription effects cannot be separated confidently.
- The analysis does not establish causation. Findings should be validated with additional data and controlled business tests.

## How to Run

### Python notebook
1. Clone or download the repository.
2. Install the required Python packages:
   ```bash
   pip install pandas sqlalchemy psycopg2-binary python-dotenv jupyter
   ```
3. Open the notebook in Jupyter.
4. Update the CSV path if your local folder structure differs.
5. Configure PostgreSQL connection details through environment variables in a local `.env` file:
   ```text
   DB_USERNAME=your_username
   DB_PASSWORD=your_password
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=your_database
   ```
6. Run the notebook to clean the dataset and load the `customer` table into PostgreSQL.

**Security:** Do not commit your `.env` file or database credentials to GitHub.

### SQL analysis
1. Open the SQL script in PostgreSQL (for example, using pgAdmin).
2. Connect to the database containing the cleaned `customer` table.
3. Run the queries to reproduce the business analysis.

### Power BI dashboard
1. Open the `.pbix` file in Power BI Desktop.
2. If prompted, update the data source connection to your local data or database.
3. Refresh the report and use the filters to explore customer and category performance.

## Project Deliverables

- Raw customer shopping behaviour dataset
- Python notebook for data cleaning and feature engineering
- SQL script containing business analysis queries
- Interactive Power BI dashboard
- Business Requirements Document
- Final project report

---

**Project:** Velora – Customer Shopping Behaviour Analysis  
**Domain:** Retail & Customer Analytics  
**Focus:** Data Cleaning | Exploratory Data Analysis | SQL Analysis | Customer Segmentation | Power BI Dashboard
