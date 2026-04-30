# Customer Shopping Behavior Analysis

A comprehensive data analysis project examining customer shopping patterns, revenue trends, and behavioral insights using Databricks and Power BI.

## 📊 Project Overview

This project analyzes customer shopping behavior data to uncover actionable insights about purchasing patterns, customer segmentation, and revenue drivers. The analysis pipeline includes data cleaning, transformation, SQL-based analytics, and interactive Power BI visualizations.

## 📁 Dataset

**Source File:** `customer_shopping_behavior.csv`

**Cleaned Table:** `customer_shopping_behavior_cleaned` (Delta format)

**Key Attributes:**
* Customer demographics (age, gender, location)
* Purchase details (amount, item, category, payment method)
* Behavioral indicators (review ratings, previous purchases, subscription status)
* Shopping preferences (shipping type, discount usage, purchase frequency)
* Derived features (age groups, purchase frequency in days)

## 🔧 Data Cleaning & Preprocessing

### Cleaning Steps:

1. **Missing Value Imputation**
   * Review ratings imputed with category-wise median values

2. **Column Standardization**
   * Converted all column names to lowercase
   * Replaced spaces with underscores
   * Renamed `Purchase Amount (USD)` → `purchase_amount`

3. **Feature Engineering**
   * Created `age_group` segments: Young Adult, Adult, Middle-aged, Senior (quartile-based)
   * Mapped `frequency_of_purchases` to `purchase_frequency_days` (numeric days)

4. **Redundancy Removal**
   * Dropped `promo_code_used` (100% correlation with `discount_applied`)

5. **Output**
   * Saved cleaned data as CSV: `customer_shopping_behavior_cleaned.csv`
   * Created Delta table: `workspace.default.customer_shopping_behavior_cleaned`

## 📈 SQL Analysis Queries

### Q1: Revenue by Gender
Analyzes total revenue contribution by male vs. female customers.

### Q2: High-Value Discount Users
Identifies customers who used discounts but still spent above average.

### Q3: Top-Rated Products
Ranks the top 5 products by average customer review rating.

### Q4: Shipping Method Comparison
Compares average purchase amounts between Standard and Express shipping.

### Q5: Subscriber Value Analysis
Compares average spend and total revenue between subscribers and non-subscribers.

### Q6: Discount-Driven Products
Identifies the 5 products with the highest discount usage percentage.

### Q7: Customer Segmentation
Segments customers into New (1 purchase), Returning (2-10 purchases), and Loyal (10+ purchases).

### Q8: Category Best-Sellers
Finds the top 3 most purchased products within each category.

### Q9: Repeat Buyer Subscription Likelihood
Analyzes subscription rates among customers with 5+ previous purchases.

### Q10: Age Group Revenue Contribution
Breaks down total revenue by age group segments.

## 📊 Power BI Dashboard

### Dashboard Overview

The Power BI dashboard provides interactive visualizations of all analytical queries, enabling stakeholders to explore customer behavior insights through dynamic filtering and drill-down capabilities.

### Key Features:

**1. Executive Summary Page**
* Total revenue KPI card
* Customer count by segment
* Revenue trends over time
* Gender distribution pie chart

**2. Product Performance**
* Top-rated products bar chart
* Discount penetration heatmap by product category
* Best-selling items by category (interactive matrix)

**3. Customer Segmentation**
* Customer lifecycle funnel (New → Returning → Loyal)
* Age group revenue breakdown (stacked bar chart)
* Subscription vs. non-subscription comparison

**4. Operational Insights**
* Shipping method analysis (Standard vs. Express)
* Discount effectiveness metrics
* Repeat buyer subscription propensity gauge


### Filters & Slicers:

* Date range selector
* Category filter
* Gender filter
* Age group filter
* Location filter
* Subscription status toggle

### DAX Measures:

```dax
Total Revenue = SUM(customer_shopping_behavior_cleaned[purchase_amount])

Average Purchase = AVERAGE(customer_shopping_behavior_cleaned[purchase_amount])

Customer Count = DISTINCTCOUNT(customer_shopping_behavior_cleaned[customer_id])

Discount Rate = 
    DIVIDE(
        CALCULATE(COUNT(customer_shopping_behavior_cleaned[customer_id]), 
                  customer_shopping_behavior_cleaned[discount_applied] = "Yes"),
        COUNT(customer_shopping_behavior_cleaned[customer_id])
    )

Subscription Rate = 
    DIVIDE(
        CALCULATE(COUNT(customer_shopping_behavior_cleaned[customer_id]), 
                  customer_shopping_behavior_cleaned[subscription_status] = "Yes"),
        COUNT(customer_shopping_behavior_cleaned[customer_id])
    )
```

## 🚀 Getting Started

### Prerequisites:

* Databricks workspace (AWS)
* Python 3.x with pandas
* Power BI Desktop (for local development)
* Power BI Pro/Premium license (for publishing)


## 📊 Key Insights

* **Gender Revenue:** [Add findings after analysis]
* **Subscription Impact:** Subscribers contribute [X]% more revenue on average
* **Age Demographics:** Young Adults generate the highest total revenue
* **Discount Effectiveness:** [X]% of customers use discounts
* **Loyalty Distribution:** [X]% New, [Y]% Returning, [Z]% Loyal customers

## 🛠️ Technologies Used

* **Data Processing:** Python (pandas), PySpark
* **Storage:** Delta Lake
* **Analytics:** Databricks SQL
* **Visualization:** Power BI
* **Cloud Platform:** AWS (Databricks)

## 🔄 Refresh & Maintenance

**Data Refresh:**
* Update source CSV as needed
* Re-run Cell 1 to refresh Delta table
* Power BI dashboard auto-refreshes daily
**Query Updates:**
* Modify Cell 2 queries as business requirements evolve
* Test in Databricks before updating Power BI

