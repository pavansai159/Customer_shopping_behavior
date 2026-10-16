# Decoding Customer Shopping Behavior

An end-to-end data analytics project that turns retail transaction data into practical decisions on customer engagement, promotions and product strategy.

Tools: Python (pandas) · MySQL · Power BI · PowerPoint



## Table of Contents

1. [Business Problem](#business-problem)
2. [Project Deliverables](#project-deliverables)
3. [Dataset](#dataset)
4. [Repository Structure](#repository-structure)
5. [Workflow](#workflow)
6. [Key Findings](#key-findings)
7. [Business Recommendations](#business-recommendations)
8. [How to Run](#how-to-run)
9. [Limitations](#limitations)



## Business Problem

A leading retail company wants to understand its customers' shopping behavior in order to improve sales, customer satisfaction and long-term loyalty. Management has noticed changing purchase patterns across demographics, product categories and sales channels, and wants to know which factors (discounts, reviews, seasons, payment preferences) drive consumer decisions and repeat purchases.

Overarching question: How can the company use consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?

## Project Deliverables

| Stage | Tool | What was done |
|---|---|---|
| Data preparation and modeling | Python | Cleaned and transformed the raw dataset |
| Data analysis | SQL | Structured the data and ran queries on customer segments, loyalty and purchase drivers |
| Visualization and insights | Power BI | Built an interactive dashboard of key patterns and trends |
| Report and presentation | PowerPoint | Summarized findings and recommendations for stakeholders |
| Repository | GitHub | Scripts, queries and dashboard files in one place |

Dataset

- Raw file: `customer_shopping_behavior.csv`
- Cleaned file:`customers_cleaned.csv`
- Size: 3,900 customer records

| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `age`, `gender`, `location` | Customer demographics |
| `item_purchased`, `category` | Product bought (25 distinct items across 4 categories) |
| `purchase_amount` | Purchase value in USD |
| `size`, `color`, `season` | Product and seasonal attributes |
| `review_rating` | Customer rating of the product |
| `subscription_status` | Whether the customer is subscribed |
| `shipping_type` | Shipping option chosen |
| `discount_applied` | Whether a discount was used |
| `previous_purchases` | Number of earlier purchases |
| `payment_method` | Payment type used |
| `frequency_of_purchases` | How often the customer buys |
| `age_group` | Engineered: age quartile band |
| `purchase_frequency_days` | Engineered: purchase frequency converted to days |

## Repository Structure

```
Customer_shopping_behavior/
├── base_file.ipynb                  # Python data cleaning and feature engineering
├── customer_shopping_behavior.csv   # Raw dataset
├── customers_cleaned.csv            # Cleaned dataset (output of the notebook)
├── project_sql.sql                  # SQL business-question queries
├── project_da.pbix                  # Power BI dashboard
├── problem_statement.txt            # Business problem
├── deliverables.txt                 # Project deliverables
└── README.md
```

## Workflow

### 1. Data preparation (Python, `base_file.ipynb`)

- Loaded the raw CSV and inspected its structure with `head`, `describe` and null counts.
- Filled missing **review ratings** with the **median rating of each product category**.
- Standardized column names to lowercase snake_case and renamed `purchase_amount_(usd)` to `purchase_amount`.
- **Feature engineering:**
  - `age_group`: customers split into four quartile-based groups (Young Adult, Adult, Middle Aged, Senior).
  - `purchase_frequency_days`: purchase frequency text (Weekly, Monthly, Quarterly and so on) mapped to a number of days.
- Dropped `promo_code_used` after confirming it was identical to `discount_applied`.
- Exported the result to `customers_cleaned.csv`.

### 2. Data analysis (SQL, `project_sql.sql`)

The cleaned data was loaded into a MySQL table named `customers`, and ten business questions were answered:

1. Total revenue by gender
2. Customers who used a discount but still spent above the average purchase amount
3. Top 5 products by average review rating
4. Average purchase amount: Standard vs Express shipping
5. Spend and revenue: subscribers vs non-subscribers
6. Top 5 products by share of purchases with a discount
7. Customer segmentation into New, Returning and Loyal
8. Top 3 most purchased products in each category
9. Whether repeat buyers (more than 5 previous purchases) tend to subscribe
10. Revenue contribution by age group

### 3. Visualization (Power BI, `project_da.pbix`)

An interactive dashboard that lets stakeholders explore spending, discounts, subscriptions, reviews, age groups and product demand. Open the file in Power BI Desktop to explore it.

## Key Findings

Headline figures: **3,900 records**, **$233,081** total recorded purchase value, **$59.76** average purchase.

- **Gender:** Male customers account for about 68% of revenue ($157,890) and Female customers about 32% ($75,191), mostly because there are about twice as many male customers in the data. Average spend per purchase is similar (about $59.54 male vs $60.25 female).
- **Subscriptions:** Subscribers (1,053) and non-subscribers (2,847) spend almost the same per purchase (about $59.49 vs $59.87). Non-subscribers generate more total revenue because there are more of them.
- **Shipping:** Average purchase amounts range only from about $58.46 (Standard) to $60.73 (2-Day Shipping). Express averages $60.48, slightly above Standard.
- **Age groups:** Young Adults contribute the most revenue ($62,143), followed by Middle Aged ($59,197), Adult ($55,978) and Senior ($55,763).
- **Customer segments:** Using the SQL definition (1 previous purchase = New, 2 to 10 = Returning, more than 10 = Loyal), most customers are Loyal (3,116), with 701 Returning and 83 New.
- **Product ratings:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80) and Handbag (3.78) have the highest average ratings.
- **Discounts:** 43% of purchases used a discount. Hat (50%), Sneakers (49.7%), Coat (49.1%), Sweater (48.2%) and Pants (47.4%) have the highest discount rates.
- **Categories:** Clothing is the largest category by revenue ($104,264), followed by Accessories ($74,200), Footwear ($36,093) and Outerwear ($18,524).
- **Repeat buyers:** Among customers with more than 5 previous purchases, 958 are subscribed and 2,518 are not, so most repeat buyers are not yet subscribers.

## Business Recommendations

1. **Grow the subscription base among repeat buyers.** Most repeat buyers are not subscribers, so they are a ready target for subscription offers.
2. **Review discount depth on heavily discounted products** such as Hat, Sneakers and Coat, and test whether lower discounts hold sales.
3. **Promote top-rated products** (Gloves, Sandals, Boots) in campaigns and use their ratings as social proof.
4. **Target Young Adults and Middle Aged groups**, the largest revenue contributors, with tailored marketing.
5. **Strengthen engagement for the small New segment** (83 customers) to move them into the Returning group.
6. **Investigate lower-rated products** to find experience problems before they affect loyalty.

## How to Run

1. **Python:** Install the requirements and run the notebook.
   ```bash
   pip install pandas numpy scikit-learn jupyter
   jupyter notebook base_file.ipynb
   ```
   Place `customer_shopping_behavior.csv` in the same folder as the notebook.
2. **SQL:** Create a database, import `customers_cleaned.csv` into a table named `customers`, then run the queries in `project_sql.sql`.
3. **Power BI:** Open `project_da.pbix` in Power BI Desktop.

## Limitations

- Results are **descriptive** and based on one supplied dataset. They do not prove causation or predict future performance.
- Differences between groups (for example subscribers vs non-subscribers) are small, so any action based on them should be tested first.
- The loyalty segments are defined by simple thresholds on `previous_purchases` and could be refined.

---

*Author: Pavan Sai*
