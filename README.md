## Retail Analytics Dashboard – Sales, Profitability & Customer Insights (Power BI)

Tools: Power BI • DAX • Power Query • SQL
Domain: Retail | Sales, Profitability, Regional & Customer Analytics
Pages: 4 (Sales-Profit Analysis • Regional Performance • Profitability • Customer Performance)


## Overview

A comprehensive 4-page Power BI dashboard analyzing $2.30M in retail sales across 5,009 orders (2014–2017). Goes beyond standard sales reporting — uses scatter plot quadrant analysis to identify margin inefficiency, maps regional profit efficiency, and tracks customer acquisition vs retention trends.

## Central business questions:
Which products generate high revenue but destroy margin?

Which regions are sales-efficient vs profit-efficient?

Is the business acquiring new customers or relying on existing ones?

Which customer segments drive the most profit?



## Dashboard Pages

## Page 1 — Sales Profit Analysis

![Sales](Screenshots/Sales.png)

KPIs: Total Sales $2.30M • Total Profit $286.34K • Profit Ratio 12.46% • Total Orders 5,009 • Return Rate 6%
Sales and Profit Trend (2014–2017) — steady YoY growth across both metrics
Profit by Category — Technology leads at $31K, Furniture near zero
Orders vs Returns Trend — returns growing alongside orders, rate stable at ~6%
Written insights embedded directly in dashboard



## Page 2 — Regional Performance
![Regional Performance](Screenshots/Region.png)


KPIs: Total Sales $2.30M • Total Profit $286.34K • Profit Ratio 12.46% • Top Region: West
Sales Distribution Across State — Bing map with bubble sizing by sales volume
Sales vs Profit by Region — West leads both at $0.73M sales / $0.11M profit
Sales vs Profit Efficiency Scatter — identifies regions where high sales don't translate to high profit
Key finding: Central region underperforms on margin despite moderate sales volume



## Page 3 — Profitability
![Profitability](Screenshots/Profitability.png)


KPIs: Total Sales $2.30M • Total Profit $286.34K • Profit Ratio 12.46% • High Sales/Low Profit Items: 11
Scatter Plot Quadrant Analysis — plots every sub-category across 4 profitability zones:

High Profit / High Sales — ideal products
High Profit / Low Sales — growth opportunity
Low Profit / High Sales — margin risk — 11 items flagged
Low Profit / Low Sales — candidates for discontinuation

Sub-category Profit Ratio Table with color-coded heat indicators and flag alerts
Key findings:

Copiers: highest profit ratio at 37%
Paper: 43% profit ratio — best margin in Office Supplies
Supplies: -$1,187 profit — loss-making sub-category identified
Furniture overall: only 2% profit ratio despite significant sales volume

## Page 4 — Customer Performance
![Customer Performance](Screenshots/Customer.png)

KPIs: Total Customers 793 • Top Customer: Tamara Chand • Avg Profit/Customer $361.08 • Avg Sales/Customer $2.90K • Retention Rate 49%


Customer Type Segmentation — High Value 35.18% / Low Value 34.55% / Medium Value 30.26%
Top 10 Customers by Profit Contribution — Tamara Chand leads at $9K
Customer Growth vs Retention Trend — returning customers increasing YoY
Key findings:

Retention rate at 49% — business increasingly dependent on existing customers
New customer acquisition declining while returning customers grow
Risk: growth strategy relies on retention, not acquisition

Paste this exactly:

## Data Model

| Table | Description |
|---|---|
| `Orders` | Core fact table — Order ID, Customer ID, Customer Name, Customer Type, Customer Category, Product ID, Product Name, Category, Profit, Quantity, Discount, Region, City, Country, Order Date, Year |
| `People` | Regional dimension — Person (manager), Region |
| `Returned` | Returns fact — Order ID, Returned flag |


## Key DAX Measures

Profit Ratio
Profit Ratio = DIVIDE([Total Profit], [Total Sales], 0)

Return Rate
Return Rate = DIVIDE([Returned Orders], [Total Orders], 0)

Customer Retention Rate
Retention Rate =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Orders[Customer ID]),
        FILTER(Orders, Orders[Customer Type] = "Returning")
    ),
    DISTINCTCOUNT(Orders[Customer ID]),
    0
)

High Sales Low Profit Flag
High Sales Low Profit Items =
CALCULATE(
    DISTINCTCOUNT(Orders[Product Name]),
    Orders[Sum of Sales] > [Sales Midpoint],
    Orders[Profit ($)] < [Profit Midpoint]
)


## Key Insights

Technology drives profit — $145K total, 17% ratio; Copiers alone at 37% margin
Supplies is loss-making — negative profit ($-1,187) despite active sales — needs pricing or discontinuation review
Furniture margin crisis — $0.73M in sales but only 2% profit ratio — high volume, low return
11 High Sales/Low Profit products identified — actionable list for margin improvement
West region dominates both revenue ($0.73M) and profit ($0.11M)
Central region margin gap — comparable sales to South but lower profit efficiency
49% retention rate — healthy but new customer acquisition declining, signaling growth risk
Top 10 customers contribute disproportionately — Tamara Chand alone at $9K profit

## Tableau Version
Interactive Tableau dashboard: [View on Tableau Public](https://public.tableau.com/app/profile/kavitha.seetharaman/viz/Online-Retail-Store-Sales-Profitability-Analysis/Dashboard1)

## Dataset

Online Retail Superstore dataset — publicly available on Kaggle.
Contains 4 years of US retail orders (2014–2017) across Technology, Office Supplies, and Furniture categories with customer segmentation and regional breakdown.

## Notes
Built during a career break to deepen end-to-end data analyst skills. This project applies quadrant analysis and customer segmentation techniques directly applicable to retail business intelligence and profitability management roles.
