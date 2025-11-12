Sales Data Analysis
Live Dashboard
Link: https://app.powerbi.com/groups/me/reports/d5d4af71-aec4-4bc5-8e05-6f7cac9e1b55?ctid=f31dc422-b277-4808-a4b8-e6cb40b25087&pbi_source=linkShare&bookmarkGuid=d4b3f2ff-3137-4afe-98e2-84df6264d4d9

Overview
An interactive Power BI report analyzing sales performance across products, time periods, and cities. It enables users to identify top/bottom performers, compare any two selected periods, and assess how discounts influence profit and units sold. The source was raw data that underwent data cleaning and formatting to ensure valid dates, standardized categories, and reliable numeric fields.

Hero Screenshot
![Image](https://github.com/user-attachments/assets/72d61b8b-42ce-4319-8adc-99eaa4d6b413)

Objectives

Identify Top/Bottom 5 products by Sales, Profit, and Quantity Sold.

Analyze time-based trends at daily, monthly, quarterly, and annual grains.

Visualize the relationship between Sales and Profit.

Compare Sales/Profit/Quantity Sold between two user-selected periods.

Track Average Discount by discount category and Total Orders.

Provide order-level detail for Sales/Profit/Discount/Net Sales and other fields filterable by Product/Date/Customer ID/Promotion Categories.

Show Sales by city.

Data and Modeling

Source: Raw sales data; cleaned and formatted in Power Query (types, nulls, category normalization, date validation).

Date modeling: Two separate date tables. Date Table 1 is the active relationship for standard reporting; Date Table 2 is used for comparisons via USERELATIONSHIP in specific measures.

Key fields: Sales, Profit, Units Sold, Discount, City, Product, Customer ID, Promotion Category, Dates.

Key Visuals

Line Chart: multi-grain trend analysis (daily/monthly/quarterly/annual).

Clustered/Stacked Column Chart: Top/Bottom 5 products and period comparisons.

Scatter Chart: relationship between Sales and Profit.

Map: Sales by city.

Cards: KPIs like Total Orders and Average Discount.

Pages

Page 1 – Overview: Profit vs Net Sales, Total Orders, Average Discount, Sales trend by period, City map.

Page 2 – Top/Bottom 5: Product analysis across Sales/Profit/Units with Top/Bottom perspective.

Page 3 – Comparison: Side-by-side Sales and Profit for two selected periods.

Page 4 – Orders Table: Detailed table of Sales/Profit/Discount/Net Sales and all remaining fields, filterable via four dynamic slicers (values update with context).

Filters and Interactions

Global slicers: Product, Date, Customer ID, Promotion Category (dynamic values update with current context).

Period comparison: Dual-date context using measures that temporarily activate Date Table 2 via USERELATIONSHIP.

Key DAX Measures
Sum Of Net Sales =
CALCULATE(
SUM('Fact'[Net Sales]),
ALL('Date Table 1'),
USERELATIONSHIP('Date Table 2'[Date], 'Fact'[Date (dd/mm/yyyy)])
)

Sum Of Profit =
CALCULATE(
SUM('Fact'[Profit]),
ALL('Date Table 1'),
USERELATIONSHIP('Date Table 2'[Date], 'Fact'[Date (dd/mm/yyyy)])
)

Sum Of Unit Sold =
CALCULATE(
SUM('Fact'[Units Sold]),
ALL('Date Table 1'),
USERELATIONSHIP('Date Table 2'[Date], 'Fact'[Date (dd/mm/yyyy)])
)

Business Questions Answered

Which products lead or lag across Sales, Profit, and Units? Action: prioritize inventory and campaigns for top performers; reassess pricing or discount levers for laggards.

How do trends behave across daily/monthly/quarterly/annual views? 
Action: align marketing and stocking with peaks; address troughs with targeted promotions.

Do higher Sales translate into higher Profit? 
Action: identify low-margin, discount-heavy items; refine discount strategy and control costs.

Which cities contribute most to sales? 
Action: focus regional promotions and field sales on high-potential cities; investigate underperformers.

Before/After (Baseline vs Result)

Baseline: Static monthly views, limited drill-through, no user-driven period comparison.

Result: Dynamic Top/Bottom analysis, dual-period comparison, city-level mapping, and order-level drill-through, improving speed-to-insight and decision-making.

Performance and Quality

Modeling: Star schema, measures-over-columns pattern, consistent naming, minimized high-cardinality fields in visuals.

DAX: Reuse base measures; avoid unnecessary bidirectional filters; use USERELATIONSHIP only inside targeted comparison measures.

Visual tuning: Apply Top N filters; limit heavy cross-interactions; simplify tooltips; keep visuals focused per page.

How to Run

Open the .pbix (or .pbip) in the latest Power BI Desktop.

Choose two date ranges using the provided selectors to enable comparison measures.

Use slicers (Product, Date, Customer ID, Promotion Category) to narrow focus; navigate to the Orders Table for granular validation and drill-through.

Credits
Author: Ganesh Singh. 

Thanks to community patterns and sample designs for inspiration.



