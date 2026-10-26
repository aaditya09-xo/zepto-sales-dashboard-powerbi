# Zepto Sales Dashboard (Power BI)

An interactive Power BI dashboard built on a Zepto sales dataset. I wanted to see which categories, cities and products bring in the most revenue, and whether discounts and influencer activity actually make a difference.

![Dashboard](dashboard.png)

## About the data

- 300 rows, 9 columns, no missing values
- 10 products across 6 categories, sold in 6 cities
- Columns: Product Name, Category, City, Original Price, Current Price, Discount, Orders, Total Revenue, Influencer Active

Overall: **50,446 orders** and **₹5.78M revenue**.

## What I did

1. Loaded the CSV into Power BI and cleaned it in Power Query (fixed data types, renamed columns).
2. Added a `Discount_Band` column (No Discount / 5% Off / 10% Off) so discounts are easier to read in charts.
3. Wrote the DAX measures below.
4. Built the dashboard: 5 KPI cards, 4 charts, a donut chart and 3 slicers (Category, City, Influencer Active).

## DAX measures

```
Total Revenue = SUM(zepto_sales_dataset[Total_Revenue])

Total Orders = SUM(zepto_sales_dataset[Orders])

Revenue per Order = DIVIDE([Total Revenue], [Total Orders])

Avg Discount % = DIVIDE(AVERAGE(zepto_sales_dataset[Discount]), 100)

Influencer Revenue =
CALCULATE([Total Revenue], zepto_sales_dataset[Influencer_Active] = "Yes")

Influencer Share % = DIVIDE([Influencer Revenue], [Total Revenue])
```

## What the data shows

- **Snacks** is the biggest category at ₹1.71M, about 30% of total revenue.
- **Hyderabad** is the top city at ₹1.25M. Mumbai is the lowest at ₹0.80M.
- **Coca Cola 1L** is the top product at ₹0.71M. The top 5 products are close to each other (₹0.58M to ₹0.71M).
- Orders with **no discount** averaged **₹125** per order. At 5% off it was ₹112, and at 10% off it was ₹106.
- Influencer-active products made up **28.8%** of revenue. Revenue per order was only slightly higher with influencers (about ₹117 vs ₹114), so I wouldn't read much into it.

I compared discounts using revenue per order and not total revenue, because the number of rows in each discount group is different (107, 91 and 102).

## Things to keep in mind

- There is **no date column**, so there is no trend or seasonality analysis.
- In 220 of the 300 rows, Current Price is higher than Original Price. I kept the data as it is.
- Total Revenue does not exactly match Current Price × Orders, so I used Total Revenue as given.
- Avg Discount is a simple average across rows, not weighted by orders.
- The discount result only shows a pattern in this dataset. It does not prove that discounts reduce order value.

## Files

| File | Description |
|------|-------------|
| `Zepto_Sales_Dashboard.pbix` | Power BI report |
| `zepto_sales_dataset.csv` | Source data |
| `dashboard.png` | Dashboard screenshot |

To open the report, download the `.pbix` file and open it in Power BI Desktop (free).

## Tools

Power BI, Power Query, DAX

## About me

[Aaditya Kumar Kushwaha], BBA graduate, working towards a role as a Data & Financial Analyst.
LinkedIn: https://www.linkedin.com/in/aaditya-kushwaha-107524340?utm_source=share_via&utm_content=profile&utm_medium=member_android)
