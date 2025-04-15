# Drinks-sales
# 📊 Power BI Sales Insights Dashboard  This project is a one-page Power BI dashboard built to deliver comprehensive **sales insights** across multiple years, geographies, products, and sales reps. It was developed from a Business Requirement Document (BRD) and designed to be scalable, automated, and insightful for business decision-making. 



---

## 🧠 Objectives

- Create an automated data ingestion pipeline for annual sales files.
- Transform and model data to support rich visual analytics.
- Build dynamic and interactive visuals to showcase:
  - Revenue performance
  - Cost analysis
  - Gross profit trends
  - Geo-distribution of sales
  - Product-level breakdown

---

## ⚙️ Power BI Implementation

### 🟩 Data Sources

- **Sales Data**: Excel files per year
- **Product Data**: CSV / Database
- **SalesRep, Category, SubCategory**: Excel
- **Geography**: Excel
- **Calendar Table**: Pre-loaded in `.pbix`

### 🛠️ Power Query Transformations

- Merged all yearly sales files into a **Sales fact table** using folder ingestion.
- Applied custom function to clean IDs:
  ```m
  let CleanID = (idText as text) => Text.Replace(idText, "ID - ", "")
  in CleanID

Data Model
Fact Table: Sales

Dimensions:

Product

Category / SubCategory

Geography

SalesRep

Calendar

Key DAX Measures
-- Total Revenue
Total Revenue = SUMX(Sales, Sales[Units] * RELATED(Product[Retail Price]))

-- Total Cost
Total Cost = SUMX(Sales, Sales[Units] * RELATED(Product[Standard Cost]))

-- Gross Profit
Gross Profit = [Total Revenue] - [Total Cost]

-- Gross Profit MoM %
Gross Profit MoM % = 
VAR CurrentMonth = [Gross Profit]
VAR PrevMonth = CALCULATE([Gross Profit], DATEADD('Calendar'[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth)

-- Average Sales Per Day
AVG Sales per Day = 
AVERAGEX(
    VALUES(Sales[Date]), 
    CALCULATE([Total Revenue])
)

-- Gross Profit QoQ %
Gross Profit QoQ % = 
VAR CurrentQ = [Gross Profit]
VAR PrevQ = CALCULATE([Gross Profit], DATEADD('Calendar'[Date], -1, QUARTER))
RETURN DIVIDE(CurrentQ - PrevQ, PrevQ)

Dashboard Design
The report features a one-page layout with:

KPI Cards: Revenue, Cost, Gross Profit

Line Charts: Monthly Profit Trends

Bar Charts: Sales by Category/SubCategory

Map: Revenue by Country/City

Decomposition Tree: Product-level Breakdown

Matrix: SalesRep vs Product performance

Slicers: Year, Quarter, Category


Automation & Scalability
Adding new yearly files to the sales folder is seamless – auto-detected during refresh.

Removing files doesn't break the model due to Power Query error handling.

The built-in calendar supports time-intelligence features out of the box.




<img width="410" alt="image" src="https://github.com/user-attachments/assets/f9318c02-cd96-4e3e-8213-919ad16b7476" />
