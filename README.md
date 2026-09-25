# Introduction

After completing an in-depth course on applying SQL to data analysis—a field I am deeply passionate about—I wanted to challenge myself with a realistic, multi-table e-commerce dataset to sharpen my analytical skills as an aspiring Data Analyst. To bridge theory with real-world business decision-making, I undertook an end-to-end analysis of the **Maven Fuzzy Factory** dataset using Google BigQuery.

Maven Fuzzy Factory is a growing e-commerce business specializing in custom plush toys. This project evaluates raw operational and transactional data to extract actionable business insights across website traffic performance, marketing channel efficiency, customer basket cross-selling behavior, and net product profitability—accounting for Cost of Goods Sold (COGS) and refund losses.

# Background

The Maven Fuzzy Factory database simulates a fast-growing online retail company over several years of expansion. As the company introduced new products and marketing channels, leadership needed data-driven clarity on site traffic, conversion efficiency, basket sizes, and actual profitability.

To answer these core business questions, the project utilizes five relational tables within Google BigQuery:
* `website_sessions`: Pageviews, session timing, traffic sources, and marketing campaigns.
* `orders`: Order IDs, session links, total revenue, and overall item counts.
* `order_items`: Granular item-level purchases, price per unit, and individual product COGS.
* `order_item_refunds`: Timestamped product refund records and refunded amounts in USD.
* `products`: Product catalog mapping `product_id` to `product_name`.

### Core Business Problems Solved:
1. **Traffic & Conversion Tracking:** Measuring monthly sessions, order volumes, and conversion rates across paid and organic traffic channels.
2. **Product Sales & Cross-Sell Behavior:** Tracking product adoption over time and calculating multi-product checkout likelihoods (e.g., probability of purchasing Product 2 alongside Product 1).
3. **Net Financial Performance:** Building modular SQL models to calculate true net revenue and net profit per product after deducting production costs (COGS) and customer refund losses.

# Tools I Used

* **Google BigQuery (BigQuery Sandbox):** My main workspace for the heavy lifting. I used BigQuery to write multi-step CTEs, window functions (`SUM() OVER()`), conditional aggregations (`MAX(IF(...))`), and `SAFE_DIVIDE()` to handle complex join logic and calculate exact product metrics.
* **Google Sheets:** Used for quick initial data checks and making sure my math and logic made sense before writing the full SQL queries in BigQuery.
* **SQL (BigQuery Dialect):** The core language I used to query the relational tables, clean up refund loss overlaps, and run multi-product basket analysis.
* **GitHub:** Used to host my repository, store my raw SQL scripts, organize project assets, and document the entire analytical process.

# The Analysis

### 1. Monthly Website Traffic & Conversion Rate Trends

**Business Question:** How have site traffic, order volumes, and conversion rates evolved on a monthly basis since launch?

![Monthly Traffic and Conversion Rate Graph](sql/trend_in_website_sessions_and_order_volumes)

**Key Findings:**
* **Conversion Rate More Than Doubled:** CVR started at **3.19%** in March 2012 and steadily climbed to a peak of **8.69%** in February 2015. This steady upward trend shows that site improvements, UX tweaks, and product expansion drastically improved traffic quality and checkout efficiency over time.
* **Massive Traffic Scaling:** Monthly sessions scaled over **15x**, growing from 1,879 sessions in March 2012 to a peak of 29,722 sessions in December 2014.
* **Strong Q4 Seasonality:** The business experiences huge end-of-year holiday surges every November and December. For example, in Q4 2014, monthly order volume crossed 2,000+ orders for the first time (2,314 orders in Dec 2014 alone).

# Conclusion
