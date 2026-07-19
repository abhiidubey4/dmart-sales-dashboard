# 🛒 DMart Retail Sales Analytics Dashboard

An end-to-end **Power BI dashboard** built on a 25,000-row retail transaction dataset, designed to help
a business understand sales performance, product trends, customer behavior, and store locations —
all in one interactive report.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

DMart (Avenue Supermarts) generates huge volumes of order-level data every day. Raw transaction rows
in a spreadsheet don't answer business questions on their own. This project turns that raw data into
a **self-service, interactive dashboard** so anyone can explore sales, products, customers, and
locations — and drill down by category, state, subscription tier, etc. — without writing a single query.

## 🎯 Business Problem

- Which product categories and cities generate the most revenue?
- Which customer segments (gender, age, subscription tier) are most valuable?
- How much revenue is lost to cancelled/returned orders?
- Which marketing channels actually drive orders?
- How are discounts affecting revenue and average order value?
- Where are customers geographically concentrated?

## 🗂️ Dataset

| Detail | Value |
|---|---|
| File | `Dmart_Dataset_Tableau.csv` |
| Rows | 25,000 order-level records |
| Columns | 29 |
| Date range | Jan 2021 – Dec 2023 |
| States covered | Maharashtra, Andhra Pradesh, Gujarat, Telangana |
| Cities covered | 40 |
| Unique products | 22 |

**Key fields:** Customer ID, Product ID, Order ID, Customer Age, Gender, Product Name, MRP,
Discount Price, Category, State, City, Subscription, Order Status, Payment Method,
Marketing/Advertisement, Order/Delivery/Cancellation Date, Rating, Time Spent on Website,
No of Clicks, Shipping Charges.

## 🛠️ Tools & Tech Stack

- **Microsoft Power BI Desktop** — data modeling, DAX measures, report building
- **Power Query** — data cleaning and transformation
- **DAX** — custom KPI/measure creation
- **CSV (Tableau-format dataset)** — data source

## 📊 Dashboard Structure (6 Pages)

| Page | Description |
|---|---|
| **Home Page** | Landing page with logo and navigation buttons to every other page |
| **Dashboard** | Executive overview — KPI cards, location map, monthly orders trend, funnel, slicers |
| **Transaction** | Order & payment status breakdown (Delivered/Cancelled/Returned, payment methods) |
| **Our Locations** | Map showing order distribution across cities and states |
| **Product Analysis** | Product performance — rating vs sales, category/subscription split, discount trend |
| **All Measures** *(hidden)* | QA page used to verify every DAX measure before hiding it from the final view |

## 🧮 Key DAX Measures

```dax
Sales = SUM('Dmart+Dataset_Tableau'[Discount Price])

Total Orders = COUNT('Dmart+Dataset_Tableau'[Order ID])

Average Discount =
AVERAGE(
    1 - ('Dmart+Dataset_Tableau'[Discount Price] / 'Dmart+Dataset_Tableau'[MRP])
)

Total Customers = DISTINCTCOUNT('Dmart+Dataset_Tableau'[Customer ID])
```

Other measures include: Average Rating, Average Order Value, Male/Female %, Total Freepass/Premium
Subscription, Customer Conversion Rate, Total Clicks, Total Shipping Charges.

## 💡 Key Insights

- 🏆 **Local products** generate ~50% of total revenue (₹91.8L), ahead of Branded and Imported.
- 📱 **Instagram** is the top marketing/acquisition channel — 8,520 orders, ₹62.4L in revenue.
- ⚠️ **~12.5% of orders** are cancelled or returned, representing ₹23L+ in at-risk revenue.
- 💳 **Freepass** customers drive the highest order volume, while Premium/Premium Plus customers
  show richer average order value.
- 🗺️ Orders are concentrated around Mumbai/Pune/Nashik and the Hyderabad/Telangana belt.
- 💰 Average discount applied: **~27%** off MRP | Average order value: **₹735.6**

## 🐞 Real Issues Fixed During Development

| Issue | Root Cause | Fix |
|---|---|---|
| Scatter chart showed negative billions on Y-axis | `Sales` measure wrongly treated Discount Price as a % instead of final price | Simplified DAX to `SUM(Discount Price)` |
| Category slicer showed only a tiny unreadable icon | Visual was too small to render its list | Resized visual, switched to list/checkbox style |
| KPI cards had oversized numbers | Default callout font too large | Reduced font size in Format pane |
| Green background bleeding around map visual | Map didn't span full page; background was green | Set page background to white, resized map to fill space |
| Duplicate/misspelled measures (`subcription`, `Revenu`) | Naming inconsistency during model building | Identified and flagged for clean-up |

## 🚀 Future Improvements

- [ ] Clean up duplicate/misspelled measure names
- [ ] Replace the legacy Q&A visual with Power BI Copilot (Q&A retires Dec 2026)
- [ ] Add a Year → Quarter → Month date hierarchy drill-down
- [ ] Add customer cohort/retention analysis

## 📁 Repository Contents
