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


