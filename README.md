# Brazilian E-Commerce Intelligence System

Multi-dimensional analysis of 100K+ orders from the Olist marketplace (2016–2018), covering customer segmentation, delivery performance, product analytics, geographic intelligence, and predictive modeling.

## Dataset

Uses the [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — 9 interconnected tables: orders, order items, customers, products, sellers, reviews, payments, geolocation, and a Portuguese-to-English product category name translation file. Tables are linked through `order_id`, `customer_id`, `product_id`, `seller_id`, and `zip_code` as shown in the notebook's ER diagram.

## Analysis Pipeline

**Data Cleaning & Feature Engineering** — Converts 5 order timestamps and 2 review timestamps to datetime. Engineers `delivery_time_days`, `estimated_vs_actual`, `processing_time_days`, and `shipping_time_days`. Extracts year, month, weekday, and hour for seasonality analysis.

**Master Dataset** — Aggregates order items per order (item count, total price, total freight, unique sellers) and payments per order (dominant type via mode, max installments, total value). Left-joins these with reviews and customer location onto the orders table.

**Exploratory Data Analysis** — KPI dashboard (total revenue, order count, AOV, unique customers, mean review score, delivery success rate) via Plotly indicators. Monthly growth trends for revenue, orders, AOV, and customer acquisition. Day-of-week and hourly seasonality patterns with a day × hour heatmap.

**RFM Customer Segmentation** — Quintile-based R/F/M scoring (1–5) mapped to 11 segments: Champions, Loyal Customers, Potential Loyalists, New Customers, Promising, Need Attention, About to Sleep, At Risk, Cannot Lose Them, Hibernating, and Lost.

**Geographic Analysis** — State-level aggregation of orders, revenue, delivery time, and review scores. City-level top 20 by revenue. Capital vs. non-capital comparison on orders, revenue, and delivery performance.

**Delivery Performance** — Categorizes deliveries into 5 tiers (Excellent ≤5 days through Very Poor >20 days). Computes on-time rate via `estimated_vs_actual ≤ 0`. Analyzes delivery-time impact on review scores with Pearson correlation.

**Product & Category Analysis** — Merges products with English category translations, then joins with order items, orders, and reviews (delivered only). Pareto analysis identifying how many products account for 80% of revenue. Monthly revenue trends for top 5 categories with seasonality scoring (coefficient of variation).

**Review Text Analysis** — Extracts top frequent words (≥4 characters, regex tokenized) separately for negative (1–2 star) and positive (4–5 star) reviews. Ranks categories by average review score filtered to >100 reviews.

**Predictive Analytics**
- *Churn Prediction:* Defines churn as Recency > 60 days. Trains Logistic Regression (scaled), Random Forest, and XGBoost (falls back to GradientBoosting if unavailable). Selects best model by F1-Score.
- *CLV Prediction:* RandomForestRegressor on monetary value (top 5% outliers removed). Segments predictions into 4 tiers via quartile binning. Reports MAE and R².
- *Demand Forecasting:* Daily revenue with 7/14/30-day moving averages. Linear trend via `scipy.stats.linregress` with 30-day forward projection.

## Tech Stack

**Python 3** — pandas, NumPy, SciPy · **Visualization** — Plotly, Matplotlib, Seaborn · **ML** — scikit-learn, XGBoost (optional) · **Text** — re, collections.Counter

## Usage

1. Download the [Olist dataset from Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).
2. Update the `data_path` variable in the notebook to your local dataset directory.
3. Run cells sequentially.

## 👤 Author

**Mehdi Hassanbeigi**  
**Email**: hasanbeigimahdi25@gmail.com 




---

##  Copyright Notice

**© 2025 Mehdi. All Rights Reserved.**

**Restrictions**:
- ❌ **No copying, modification, or distribution** of this work is permitted