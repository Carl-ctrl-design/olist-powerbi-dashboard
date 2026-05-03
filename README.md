# Olist E-Commerce Executive Dashboard — Power BI


## Project Overview

This project delivers a 5-page interactive executive dashboard built in 
Power BI Desktop, connecting live to a PostgreSQL 17 database containing 
the Olist Brazilian E-Commerce dataset. It represents the third project in 
a structured data analytics portfolio, completing a full end-to-end data 
pipeline: raw data → relational database → SQL analysis → business 
intelligence dashboard.

The dashboard transforms 100,000+ transactions across 8 relational tables 
into actionable business insights covering revenue performance, customer 
behaviour, logistics efficiency, and strategic recommendations presented 
in a format ready for executive decision-making.

## The Data Pipeline
Raw Olist Data (CSV)
↓
PostgreSQL 17 Database (8 relational tables, 100K+ rows)
↓
Power BI Desktop — Live Import Connection
↓
Power Query — Data verification and type validation
↓
Data Model — 7 relationships across fact and dimension tables
↓
DAX Measures — 10 calculated business metrics
↓
5-Page Executive Dashboard

Connecting Power BI directly to PostgreSQL rather than loading flat CSV 
files demonstrates understanding of production data pipelines. Data types 
were enforced at the database level, meaning timestamps, decimals, and 
identifiers arrived correctly typed in Power BI with zero manual 
correction required.

---

## Dashboard Pages

### Page 1 — Executive Overview
![Executive Overview](screenshots/01_executive_overview.png)

The hero page. Answers five business questions in under 10 seconds.

- **$15.84M** total revenue across the dataset period
- **99K** total orders processed
- **4.09 / 5** average customer review score
- **91.89%** on-time delivery rate
- Monthly revenue trend showing peak performance in May ($1.74M) 
  with a sharp decline in September
- Order status breakdown showing 97.02% of orders successfully delivered
- Geographic distribution map showing customer concentration in 
  southeastern Brazil

---

### Page 2 — Sales Performance
![Sales Performance](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/02.png)

Revenue analysis by product category and seller performance.

- **Health & Beauty** is the top revenue category at $1.44M, followed 
  by Watches & Gifts ($1.31M) and Bed/Bath/Table ($1.24M)
- Top seller generates $0.25M individually — significant revenue 
  concentration in a small number of high-performing sellers
- Monthly revenue column chart reveals strong H1 performance peaking 
  in May ($1.74M) with notable H2 decline, particularly in September 
  ($0.72M) — suggesting seasonal or operational disruption

---

### Page 3 — Customer Behaviour
![Customer Behavior](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/03.png)

Payment preferences, satisfaction distribution, and geographic 
concentration analysis.

- **78.34% of revenue** flows through credit card payments — 
  critical single point of payment failure risk
- Boleto (Brazilian bank slip) accounts for 17.92% — 
  significant alternative payment preference
- **São Paulo (SP)** generates 40K+ orders — more than double 
  the second largest state (RJ), revealing extreme geographic 
  concentration
- Review score distribution shows score 5 dominating but score 1 
  as a significant third-place result — revealing a polarised 
  customer satisfaction pattern

---

### Page 4 — Logistics and Delivery
![Logistics and Delivery](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/04.png)

Delivery performance analysis by state and freight cost by category.

- **Average delivery time: 3.21 days** across all delivered orders
- Northern and northeastern states (RR, SE, MA, RN, AC) show the 
  slowest delivery times at 3.4–3.7 days — reflecting geographic 
  distance from São Paulo seller concentration
- Lowest on-time delivery rates in AL (76.07%) and MA (80.33%) — 
  states that also show slow delivery times, confirming a logistics 
  performance crisis in remote regions
- **Computers** carry the highest average freight value at $48, 
  followed by home appliances ($45) and furniture categories — 
  informing seller pricing strategy decisions

---

### Page 5 — Insights and Recommendations
![Insights and Recommendations](https://github.com/Carl-ctrl-design/olist-powerbi-dashboard/blob/main/screenshots/05.png)

The analytical conclusion. Four data-driven findings mapped directly 
to four strategic recommendations — the page that separates this 
dashboard from a basic chart collection.

**Key Findings:**
1. Revenue Concentration Risk — São Paulo generates 40%+ of all orders
2. Customer Satisfaction is Polarised — 4.09 average but 1-star is 
   third most common score
3. Logistics Performance Degrades by Distance — northern states show 
   3x longer delivery times
4. Credit Card Dominance Creates Risk — 78% of revenue through 
   single payment channel

**Strategic Recommendations:**
1. Geographic Expansion — target MG, RJ, RS with growth campaigns
2. Customer Experience Recovery Program — post-delivery follow-up 
   for low-score orders
3. Northern Logistics Partnership — regional last-mile carriers 
   for PA, AM, RR states
4. Payment Diversification — incentivise boleto and PIX adoption

---

## Data Model

7 relationships across 8 tables following a star schema pattern: customers (1) ──── () orders (1) ──── () order_items () ──── (1) products
│                      │                      │
│              (1) sellers            (1) category_translation
│
() order_payments
(*) order_reviews


**Fact Tables:** orders, order_items, order_payments, order_reviews  
**Dimension Tables:** customers, products, sellers, category_translation

---

## DAX Measures

10 custom measures built in a dedicated `_Measures` table:

| Measure | Formula Pattern | Purpose |
|---|---|---|
| Total Revenue | SUMX with row-level arithmetic | Price + freight per line item |
| Total Orders | DISTINCTCOUNT | Unique order count |
| Average Order Value | DIVIDE | Safe division of revenue by orders |
| Average Review Score | AVERAGE | Customer satisfaction KPI |
| On-Time Delivery Rate | DIVIDE + COUNTROWS + FILTER | % orders delivered by estimated date |
| Monthly Revenue | CALCULATE + DATESMTD | Month-to-date revenue |
| Previous Month Revenue | CALCULATE + PARALLELPERIOD | Prior month revenue for growth calc |
| MoM Growth % | DIVIDE with measure referencing | Month-over-month growth percentage |
| Avg Delivery Days | AVERAGEX + DATEDIFF | Mean days from purchase to delivery |
| Avg Freight Value | AVERAGE | Mean shipping cost per order item |
| Payment Revenue | SUMX on order_payments | Revenue through payment channel |

---

## Technical Stack

| Tool | Version | Purpose |
|---|---|---|
| Power BI Desktop | 2.152.1279.0 (March 2026) | Dashboard development |
| PostgreSQL | 17 | Source database |
| pgAdmin | 4 | Database management |
| DAX | — | Calculated measures |
| Power Query | — | Data verification |

---

## Related Projects

This dashboard is the third project in a structured portfolio:

| # | Project | Tools | Link |
|---|---|---|---|
| 1 | Superstore Sales Analysis | Excel, PivotTables, KPI Dashboard | [View Repository](https://github.com/Carl-ctrl-design) |
| 2 | Olist SQL Analysis | PostgreSQL 17, CTEs, Window Functions | [View Repository](https://github.com/Carl-ctrl-design) |
| 3 | Olist Power BI Dashboard | Power BI, DAX, PostgreSQL | This repository |

The SQL analysis (Project 2) and this dashboard (Project 3) use the 
same Olist dataset intentionally — the SQL project provides the 
analytical foundation and this dashboard delivers the executive 
presentation layer. Together they demonstrate a complete data 
workflow from raw database queries to stakeholder-ready visuals.

---

## Dataset

**Olist Brazilian E-Commerce Public Dataset**  
Source: Kaggle — publicly available  
Size: 100,000+ orders, 8 relational tables  
Period: September 2016 to October 2018  
Geography: Brazil — 27 states

Tables: orders, order_items, order_payments, order_reviews, 
customers, products, sellers, category_translation

---

## Author

**Carl Waiti**  
BSc Economics and Finance — Kenyatta University (Final Year)  
Google Data Analytics Professional Certificate  

GitHub: [Carl-ctrl-design](https://github.com/Carl-ctrl-design)  
Portfolio: [carl-ctrl-design.github.io/C.Waiti](https://carl-ctrl-design.github.io/C.Waiti/)
