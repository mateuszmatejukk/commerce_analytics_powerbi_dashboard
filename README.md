# Commerce Analytics Power BI Dashboard

Two-page Power BI dashboard built on top of the PostgreSQL gold layer from my
https://github.com/mateuszmatejukk/commerce_analytics_mini_platform project.

## Overview

The dashboard connects directly to PostgreSQL and visualizes the sales, customer and
product data modeled in the gold and silver layers (EduCommerce dataset).

## Page 1: Sales Overview
- KPI cards: Net Revenue, Gross Revenue, Discount Share %, Orders
- Monthly net revenue trend (line chart)
- Net revenue by country (bar chart)
- Slicers: country and date range

## Page 2: Customers & Products
- Top 5 customers by net revenue (Top N filter)
- Top 3 products by net revenue, filterable by category and month (Top N filter)
- Orders by payment status (donut chart)
- Customer table with country, order count and net revenue

## Data sources

| Table | Used for |
|---|---|
| `gold.daily_sales_summary` | Revenue KPIs, trend, country breakdown |
| `gold.customer_analytics` | Top customers, customer table |
| `gold.product_performance_monthly` | Top products by category and month |
| `silver.orders_enriched` | Payment status breakdown |

## DAX measures

```
Net Revenue = SUM('gold daily_sales_summary'[net_revenue])
Gross Revenue = SUM('gold daily_sales_summary'[gross_revenue])
Discount Share % = DIVIDE(SUM('gold daily_sales_summary'[discount_value]), [Gross Revenue])
Orders = SUM('gold daily_sales_summary'[orders_count])
Orders Count = COUNTROWS('silver orders_enriched')
```

## Tools

PostgreSQL, Power BI Desktop, DAX

## Files

- `powerbi/commerce_analytics_dashboard.pbix`: Power BI report
- `images/`: dashboard screenshots
