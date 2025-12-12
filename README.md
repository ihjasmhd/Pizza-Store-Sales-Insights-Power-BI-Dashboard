# Pizza-Store-Sales-Insights-Power-BI-Dashboard
Built an interactive Power BI dashboard analyzing 2015 pizza sales, featuring KPIs, daily/monthly trends, category and size performance, and top/bottom sellers. Cleaned and modeled data using Power Query and DAX to deliver clear insights for revenue, demand, and operational decisions.

---

**Project:** Pizza Sales Performance Dashboard
**Dataset:** Pizza Sales 2015 (orders, order details, pizzas)
**Tools:** Power BI Desktop, Power Query, DAX, Excel / CSV

---

## Overview

This project analyzes pizza sales data for 2015 to surface business insights and operational trends. The dashboard provides key metrics (revenue, order counts, pizzas sold, averages) and interactive visualizations (daily/monthly trends, category/size breakdowns, top/bottom sellers) to help stakeholders optimize marketing, inventory, and staffing.

---

## Problem Statement

We need to analyze key indicators for our pizza sales data to gain insights into business performance. Specifically, calculate:

1. **Total Revenue:** Sum of total price of all pizza orders.
2. **Average Order Value:** Total revenue ÷ Total number of orders.
3. **Total Pizzas Sold:** Sum of quantities of all pizzas sold.
4. **Total Orders:** Total number of orders placed.
5. **Average Pizzas Per Order:** Total pizzas sold ÷ Total orders.

Sample summary figures (from dataset):

* Total Pizzas Sold: **49,574**
* Total Orders: **21,350**

---

## Charts Requirement (Visualizations)

Build the following charts on the dashboard:

1. **Daily Trend for Total Orders**

   * Visual: Bar chart
   * Axis: Date (day) → Value: Count of `order_id` (or aggregated orders)

2. **Monthly Trend for Total Orders**

   * Visual: Line chart
   * Axis: Month → Value: Count of `order_id` (or aggregated orders)

3. **Percentage of Sales by Pizza Category**

   * Visual: Pie/Donut chart
   * Value: Sum of `quantity` or `revenue` by `pizza_category`

4. **Percentage of Sales by Pizza Size**

   * Visual: Pie/Donut chart
   * Value: Sum of `quantity` or `revenue` by `pizza_size`

5. **Total Pizzas Sold by Pizza Category**

   * Visual: Funnel chart or Bar chart
   * Value: Sum of `quantity` grouped by `pizza_category`

6. **Top 5 Best Sellers (Revenue, Quantity, Orders)**

   * Visual: Bar chart (Top N filter = 5)
   * Metrics: Revenue, Quantity, Orders per `pizza_name`

7. **Bottom 5 Best Sellers (Revenue, Quantity, Orders)**

   * Visual: Bar chart (Bottom N filter = 5)

---

## Dataset

Expected files (example):

* `orders.csv` — order-level details (`order_id`, `order_date`, `customer_id`, `total_price`, etc.)
* `order_details.csv` — items in each order (`order_id`, `pizza_id`, `quantity`, `price`)
* `pizzas.csv` — pizza catalog (`pizza_id`, `pizza_name`, `pizza_category`, `pizza_size`, `price`)

> Adjust file names/columns per your source data. If using a single combined file (e.g., `pizza_sales_2015.csv`), the same steps apply.

---

## Tools & Technologies

* Power BI Desktop (recommended)
* Power Query (for data cleaning and split/transform)
* DAX (for measures & calculated columns)
* Excel / CSV (for raw data)

---

## Data Preparation (Power Query)

1. Load all source CSV/Excel files into Power BI.
2. Merge `orders` and `order_details` on `order_id` (if separate).
3. Ensure numeric columns (`quantity`, `price`, `total_price`) are correct data types.
4. Create `order_date` as date type; extract `day`, `month`, `weekday`, `hour` as needed.
5. Trim and standardize category/name fields (remove extra spaces).
6. Close & Apply.

---

## Recommended DAX Measures

Place these measures in your model (rename tables/columns as required):

```DAX
Total Revenue = SUM('order_details'[price] * 'order_details'[quantity])
-- or if orders table has total:
-- Total Revenue = SUM('orders'[total_price])

Total Orders = DISTINCTCOUNT('orders'[order_id])

Total Pizzas Sold = SUM('order_details'[quantity])

Average Order Value =
DIVIDE([Total Revenue], [Total Orders], 0)

Average Pizzas Per Order =
DIVIDE([Total Pizzas Sold], [Total Orders], 0)
```

Optional Top-N measures (example for revenue):

```DAX
Revenue by Pizza = SUMX(
    VALUES('pizzas'[pizza_id]),
    CALCULATE(SUM('order_details'[price] * 'order_details'[quantity]))
)
```

---

## Visualization Field Mapping & Steps

* **Daily Orders (Bar)**: Axis = `order_date` (day), Value = `Total Orders` or `COUNT(order_id)`
* **Monthly Orders (Line)**: Axis = `order_date` (month), Value = `Total Orders`
* **Sales % by Category**: Legend = `pizza_category`, Value = `Total Pizzas Sold` or `Total Revenue` (use Donut)
* **Sales % by Size**: Legend = `pizza_size`, Value = `Total Pizzas Sold` or `Total Revenue` (Donut)
* **Pizzas Sold by Category (Funnel/Bar)**: Category = `pizza_category`, Value = `Total Pizzas Sold`
* **Top/Bottom 5 Pizzas**: Use bar chart; apply Top N filter on `pizzas[pizza_name]` by measure (Revenue or Quantity). Sort descending/ascending.

Add slicers: Date range, Pizza Category, Pizza Size.

---

## UX & Design Tips

* Use a KPI card row with: Total Revenue, Total Orders, Total Pizzas Sold, Avg Order Value, Avg Pizzas/Order.
* Use consistent color palette; emphasize best-sellers with contrasting color.
* Add tooltips and drill-through to item-level details (orders by pizza).
* Add narrative text boxes summarizing insights (peak days/hours, best categories).

---

## File Structure (suggested)

```
/pizza-sales-2015/
├─ data/
│  ├─ orders.csv
│  ├─ order_details.csv
│  └─ pizzas.csv
├─ powerbi/
│  └─ Pizza_Sales_Dashboard.pbix
├─ README.md
└─ docs/
   └─ screenshots/
```

---

## How to Reproduce

1. Clone repo and open `Pizza_Sales_Dashboard.pbix` (or import CSVs into Power BI).
2. In Power Query, apply the provided transformations.
3. Create DAX measures listed above.
4. Build visuals per mapping.
5. Publish to Power BI Service (optional) and share dashboard.

---

## Insights & Business Value

The dashboard identifies peak order days and hours, best-selling pizza categories and sizes, and top/bottom products by revenue and quantity — enabling data-driven decisions for menu optimization, inventory planning, promotions, and staffing.

---

## Contribution

Contributions are welcome. Please open an issue or pull request for bug fixes, new visualizations, or dataset updates.

---

## License

Specify your license (e.g., MIT) or your organization’s standard license.

---

If you want, I can:

* Convert this README into a GitHub-flavored markdown file and include sample screenshots from your Power BI PDF.
* Produce the exact `.pbix` build steps and provide the DAX and Power Query M code to paste into Power BI. Would you like that?


