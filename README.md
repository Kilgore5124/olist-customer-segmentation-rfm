# Customer Segmentation for a Brazilian E-Commerce Company Using RFM Analysis

## Project Overview

This project uses **RFM (Recency, Frequency, Monetary)** analysis to segment customers of **Olist**, a Brazilian e-commerce platform, based on their purchasing behavior. The goal is to identify high-value customer groups to support targeted marketing strategies and improve customer retention and ROI.

---

## Business Objective

Olist wants to better understand its customer base in order to:
- Reward its most valuable customers
- Re-engage at-risk or inactive segments
- Tailor marketing efforts to behavior-based personas

---

## Dataset

The analysis uses three tables from the Olist public dataset:
- `orders`: order metadata with purchase timestamps
- `customers`: unique customer IDs
- `order_payments`: total payment value per order

The final dataset includes customer-level **recency**, **frequency**, and **monetary** metrics.

---

## Methods

- RFM scoring using **quintiles** to assign 1–5 scores
- Customer segmentation based on RFM score patterns
- Group-level analysis of average metrics by segment
- Exported clean dataset for Tableau dashboarding

All analysis was performed in **Google Colab** using:
- Python (Pandas, Matplotlib)
- Google BigQuery (for initial SQL queries)
- Gemini (for automation and documentation)

---

## Key Segments

| Segment        | Description                                 |
|----------------|---------------------------------------------|
| Champions      | Recent, frequent, high-spending customers   |
| Loyal          | Buy frequently but may spend less per order |
| At Risk        | Haven’t purchased in a while                |
| Hibernating    | Inactive and low-spending customers         |

---

## Tableau Dashboard

[🔗 Link to Tableau Dashboard Here](#) *(Replace this with your public link once published)*

---

## Recommendations

- **Champions**: Offer loyalty perks and exclusive access
- **At Risk**: Send reactivation campaigns and discounts
- **Loyal**: Encourage upsells or referrals
- **Hibernating**: Analyze acquisition cost vs. reactivation ROI

---

## How to Use

1. Run the notebook in [Google Colab](https://colab.research.google.com/)
2. View `rfm_segmented_data.csv` for ready-to-use Tableau input

---

## SQL Query

The full SQL logic used to prepare the customer-level RFM dataset is available below:

-- Step 1: Filter delivered orders and join with payments
WITH delivered_orders AS (
  SELECT
    o.customer_id,
    o.order_id,
    CAST(o.order_purchase_timestamp AS DATE) AS order_date,  -- Convert timestamp to date
    op.payment_value
  FROM
    `second-analysis.olist.orders` o
  JOIN
    `second-analysis.olist.order_payments` op
  ON
    o.order_id = op.order_id
  WHERE
    o.order_status = 'delivered'  -- Only consider delivered orders
),

-- Step 2: Find the most recent purchase date in the dataset
max_order_date AS (
  SELECT
    MAX(order_date) AS max_date
  FROM
    delivered_orders
),

-- Step 3: Aggregate data at customer level to calculate Recency, Frequency, and Monetary
customer_rfm AS (
  SELECT
    do.customer_id,
    DATE_DIFF(mo.max_date, MAX(do.order_date), DAY) AS recency_days,  -- Days since last purchase
    COUNT(DISTINCT do.order_id) AS frequency,                        -- Number of orders
    SUM(do.payment_value) AS monetary                                -- Total amount spent
  FROM
    delivered_orders do
  CROSS JOIN
    max_order_date mo  -- Bring in max purchase date to calculate recency
  GROUP BY
    do.customer_id, mo.max_date
)

-- Final output: list customers with RFM metrics ordered by recency (most recent first)
SELECT * FROM customer_rfm
ORDER BY recency_days ASC
LIMIT 100


This query:
•	Filters for delivered orders
•	Joins payment and order data
•	Calculates Recency, Frequency, and Monetary values per customer
•	Outputs a clean table ready for segmentation in Python

The query was run using Google BigQuery and served as the foundation for the RFM analysis.

