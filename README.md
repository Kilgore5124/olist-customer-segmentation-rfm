# 📊 Customer Segmentation with RFM Analysis (Brazilian E-Commerce)

This project uses real-world transactional data from a Brazilian e-commerce company (Olist) to perform **RFM-based customer segmentation**, helping identify high-value customer groups and optimize marketing strategies.

---

## 🎯 Business Objective

Customer acquisition is costly — so retaining and nurturing existing customers is crucial. This project answers:

> **"Which types of customers should the business focus on to increase retention, loyalty, and ROI?"**

We use **Recency, Frequency, and Monetary (RFM) analysis** to segment customers based on behavior and value, providing actionable insights for marketing and lifecycle management.

---

## 🛠 Tools & Technologies

- **Google BigQuery** – to query raw order and payment data  
- **Google Colab** (Python, Pandas) – for data transformation and RFM scoring  
- **Tableau** – for interactive dashboards  
- **GitHub** – for version control and portfolio presentation  

---

## 📦 Dataset

We used the public [Olist Brazilian E-Commerce dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) containing:  
- Customer orders (timestamps, status)  
- Payments (total value per order)  

We filtered for **delivered orders only**, as they represent actual completed transactions.

---

## 🧮 RFM Analysis Process

| Metric     | Description                       | Scoring           |
|------------|-----------------------------------|-------------------|
| Recency    | Days since last purchase          | Lower is better   |
| Frequency  | Number of delivered orders        | Higher is better  |
| Monetary   | Total spend (`payment_value`)     | Higher is better  |

Each metric is scored from **1 to 5** using quantiles, and combined into a **3-digit `rfm_score`** (e.g. `555`).

---

## 🏷 Customer Segments

Customers were assigned to segments using RFM score logic:

| Segment               | Criteria                        |
|-----------------------|---------------------------------|
| Champion              | R = 5, F = 5, M = 5             |
| Loyal Customer        | R ≥ 4 and F ≥ 4                 |
| Potential Loyalist    | R ≥ 3 and F ≥ 4                 |
| New Customer          | R = 5 and F ≤ 2                 |
| At Risk               | R ≤ 2 and F ≥ 4                 |
| Lost                  | R = 1 and F = 1                 |
| Other                 | Default fallback segment        |

---

## 📤 Final Output

The final dataset includes:

```csv
customer_id, recency_days, frequency, monetary, r_score, f_score, m_score, rfm_score, segment
