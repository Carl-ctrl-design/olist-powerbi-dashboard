# Olist E-Commerce Executive Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-March%202026-F2C811)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-336791)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Records](https://img.shields.io/badge/Records-100K%2B-orange)
![Pages](https://img.shields.io/badge/Pages-5-blue)

> A 5-page executive dashboard connected live to PostgreSQL 17. Revenue performance, customer behaviour, logistics efficiency, and strategic recommendations in a format ready for executive decision-making.

---

## What this is

This dashboard is the visual intelligence layer on top of the Olist SQL analysis project. It transforms 100,000+ transactions across 8 relational tables into a single executive-facing report. Power BI connects directly to PostgreSQL rather than a flat CSV file, which means data types are enforced at the database level and arrive correctly typed in Power BI with zero manual correction.

Complete data pipeline:

```
Raw Olist Data (CSV)
        |
        v
PostgreSQL 17 Database
(8 relational tables, 100K+ rows)
        |
        v
Power BI Desktop: Live Import Connection
        |
        v
Power Query: Data verification and type validation
        |
        v
Data Model: 7 relationships across fact and dimension tables
        |
        v
DAX Measures: 10 calculated business metrics
        |
        v
5-Page Executive Dashboard
```

---

## Dashboard pages

### Page 1: Executive Overview
![Executive Overview](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/01.png)

The hero page. Five headline KPIs answerable in under 10 seconds.

- **$15.84M** total revenue across the dataset period
- **99K** total orders processed
- **4.09 out of 5** average customer review score
- **91.89%** on-time delivery rate
- Monthly revenue trend showing peak performance in May ($1.74M) with a sharp September decline
- Order status breakdown: 97.02% of orders successfully delivered
- Geographic distribution map showing customer concentration in southeastern Brazil

---

### Page 2: Sales Performance
![Sales Performance](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/02.png)

Revenue by product category and seller performance.

- Health and Beauty leads revenue at $1.44M, followed by Watches and Gifts ($1.31M) and Bed, Bath and Table ($1.24M)
- Top individual seller generates $0.25M, revealing significant revenue concentration in a small number of high performers
- Monthly revenue column chart shows strong H1 peaking in May ($1.74M) with a notable H2 decline in September ($0.72M), pointing to seasonal or operational disruption

---

### Page 3: Customer Behaviour
![Customer Behaviour](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/03.png)

Payment preferences, satisfaction distribution, and geographic concentration.

- 78.34% of revenue flows through credit card payments, a single-channel concentration risk
- Boleto accounts for 17.92%, a meaningful alternative for customers without credit access
- Sao Paulo (SP) generates 40K+ orders, more than double the second largest state (RJ)
- Review score distribution shows score 5 dominating, but score 1 ranking as the third most common result. A polarised satisfaction pattern, not a generally satisfied customer base

---

### Page 4: Logistics and Delivery
![Logistics and Delivery](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/04.png)

Delivery performance by state and freight cost by category.

- Average delivery time: 3.21 days across all delivered orders
- Northern and northeastern states (RR, SE, MA, RN, AC) show the slowest delivery times at 3.4 to 3.7 days, reflecting geographic distance from the SP seller base
- Lowest on-time delivery rates in AL (76.07%) and MA (80.33%): both states also rank slowest for delivery times, confirming a logistics performance failure in remote regions, not just slow transit
- Computers carry the highest average freight value at $48, followed by home appliances ($45) and furniture, directly informing seller pricing strategy

---

### Page 5: Insights and Recommendations
![Insights and Recommendations](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/05.png)

The analytical conclusion page. Four findings mapped to four actionable recommendations. This is the page that separates a dashboard from a chart collection.

| Finding | Recommendation |
|---|---|
| SP generates 40%+ of all orders. Geographic concentration risk | Target MG, RJ, and RS with dedicated growth campaigns |
| Average review score is 4.09 but score 1 is the third most common result | Build a post-delivery recovery programme targeting low-score orders within 48 hours |
| Northern states experience delivery times 3x longer than SP | Partner with regional last-mile carriers for PA, AM, and RR states |
| 78% of revenue flows through one payment channel | Incentivise Boleto and PIX adoption to reduce single-channel dependency |

---

## Data model

Star schema with 7 relationships across 8 tables.

```
customers (1) ---- (*) orders (1) ---- (*) order_items (*) ---- (1) products
                       |                                               |
                  (*) order_payments                    (1) category_translation
                  (*) order_reviews
                       |
                  (*) sellers
```

**Fact tables:** orders, order_items, order_payments, order_reviews
**Dimension tables:** customers, products, sellers, category_translation

---

## DAX measures (10 total, all in \_Measures table)

| Measure | Formula pattern | Purpose |
|---|---|---|
| Total Revenue | SUMX with row-level arithmetic | Price plus freight per line item |
| Total Orders | DISTINCTCOUNT | Unique order count |
| Average Order Value | DIVIDE | Safe division of revenue by orders |
| Average Review Score | AVERAGE | Customer satisfaction KPI |
| On-Time Delivery Rate | DIVIDE + COUNTROWS + FILTER | Percentage of orders delivered by estimated date |
| Monthly Revenue | CALCULATE + DATESMTD | Month-to-date revenue |
| Previous Month Revenue | CALCULATE + PARALLELPERIOD | Prior month for growth calculation |
| MoM Growth % | DIVIDE with measure referencing | Month-over-month growth percentage |
| Avg Delivery Days | AVERAGEX + DATEDIFF | Mean days from purchase to delivery |
| Avg Freight Value | AVERAGE | Mean shipping cost per order item |

---

## Technical stack

| Tool | Version | Purpose |
|---|---|---|
| Power BI Desktop | 2.152.1279.0 (March 2026) | Dashboard development |
| PostgreSQL | 17 | Source database |
| pgAdmin | 4 | Database management |
| DAX | 10 measures | Calculated metrics |
| Power Query | - | Data type verification |

---

## Connected project

**Project 2: Olist SQL Analysis**
The SQL analysis project built and populated the PostgreSQL database this dashboard connects to. The two projects use the same dataset intentionally: the SQL project provides the analytical foundation and this dashboard delivers the executive presentation layer.

[View the SQL repository](https://github.com/Carl-ctrl-design/olist-sql-analysis-project)

---

## Dataset

**Source:** Kaggle, Olist Brazilian E-Commerce Public Dataset
**Size:** 100,000+ orders across 8 relational tables
**Period:** September 2016 to October 2018
**Geography:** Brazil, 27 states

---

## Portfolio context

| # | Project | Tools | Link |
|---|---|---|---|
| 1 | Superstore Sales Analysis | Excel, PivotTables, KPI Dashboard | [View](https://github.com/Carl-ctrl-design/superstore-sales-analysis) |
| 2 | Olist SQL Analysis | PostgreSQL 17, CTEs, Window Functions | [View](https://github.com/Carl-ctrl-design/olist-sql-analysis-project) |
| 3 | Olist Power BI Dashboard | Power BI, DAX, PostgreSQL | This repo |
| 4a | Safaricom SQL Financial Analysis | PostgreSQL 17, Primary Source Data | [View](https://github.com/Carl-ctrl-design/safaricom_sql_financial_analysis) |
| 4b | Safaricom Power BI Dashboard | Power BI, DAX, PostgreSQL | [View](https://github.com/Carl-ctrl-design/safaricom-powerbi-dashboard) |

---

## Author

**Carlton Waiti**, Data and Business Analyst, Nairobi, Kenya

BSc Economics and Finance, Kenyatta University (2026)
Google Data Analytics Professional Certificate

[GitHub](https://github.com/Carl-ctrl-design) · [Portfolio](https://carl-ctrl-design.github.io/C.Waiti) · [LinkedIn](https://www.linkedin.com/in/carlton-waiti)
