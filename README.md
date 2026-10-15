# Online Retail: Who Are the Most Valuable Customers?

A customer analysis of one year of real sales from a UK online gift shop, using **Python** and **SQL**.

**Open the notebook:** [`online_retail_analysis.ipynb`](online_retail_analysis.ipynb). All the code, SQL, tables and charts are in one place, top to bottom.

## The business question

Which customers bring in the most money, which customers is the shop losing, and how do sales change through the year?

## The data

- **Source:** Online Retail dataset, UCI Machine Learning Repository (details in [`data/SOURCE.md`](data/SOURCE.md))
- **Period:** 1 December 2010 to 9 December 2011
- **Size:** 541,909 rows. Each row is one product on one invoice.
- **Columns:** invoice number, product code, description, quantity, date, price, customer ID, country

## What I did

1. **Cleaned the data with pandas.** Removed duplicate rows, rows with no customer ID, cancelled orders, zero or negative prices, and postage/fee lines. 541,909 rows became 385,929.
2. **Loaded it into SQLite and answered questions with SQL.** Monthly revenue and growth, top countries, top products, and repeat customers. The queries are in [`sql/`](sql/).
3. **Grouped customers with RFM.** Each customer was scored 1–5 on Recency, Frequency and Monetary value using `NTILE(5)`, then put into four groups: Champions, Active, At risk and Lost.
4. **Made charts with matplotlib** and wrote down the findings.

## What I found

- **26% of customers (the Champions) bring 69.5% of revenue.**
- **648 customers are "At risk".** They used to order often but have not ordered for about 5 months.
- **34.9% of customers ordered only once** and never came back.
- **Sales peak in October and November**, before Christmas.
- **The UK brings about 83% of revenue.**

![Share of customers vs share of revenue](images/segments.png)

![Monthly revenue](images/monthly_revenue.png)

## Recommendations

1. Protect the Champions with a loyalty programme.
2. Send a win-back offer to the At-risk customers.
3. Follow up after a customer's first order, because a third never order again.
4. Plan stock early for the October–November peak.

## Limitations

- One shop, one year, mostly UK customers.
- No product costs in the data, so profit cannot be calculated.
- Sales with no customer ID (about a quarter of rows) are left out of the customer analysis.
- December 2011 has only 9 days of data.

## How to run it

```bash
pip install -r requirements.txt
jupyter notebook online_retail_analysis.ipynb
```

## Skills used

Python (pandas, matplotlib) · SQL (GROUP BY, CTEs, window functions: `LAG`, `NTILE`) · data cleaning · customer segmentation
