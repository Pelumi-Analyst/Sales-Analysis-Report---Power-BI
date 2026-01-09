# Sales Analysis Report
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/95a7eec2120786b8905adfdb858c6c9c55670555/Sales%20Analysis%20Report%20-%20Power%20BI%20Project.png)
---
## **Report Page Overview**
This report page provides a high-level sales performance analysis, focusing on revenue, units sold, regional performance, models, and store performance. It was designed to help business leaders and sales managers quickly understand where revenue is coming from, which regions and stores are performing best, and how sales are trending over time.
---
## **Business Questions Answered**
- What is the total revenue?
- What is the total units sold?
- Which regions contribute the most revenue?
- Which models drive unit sales?
- What are the top-performing stores by average revenue?
- How is revenue distributed across Lines of Business (LOB)?
- How does revenue and units sold change month-over-month (MoM)?
---
## **Data Preparation & Data Modeling**
The dataset used was a single flat file(Denormalized table) containing transactional sales data with columns such as Region, Market, Store, Model, Line of business, Trade Date, Revenue, and Units Sold.

To improve performance, readability, and analytical flexibility, the data was **normalized into a star schema** consisting of one Fact Table and four Dimension Tables.

_**Fact Table**_ - FactSales

_**Dimension Tables**_ - D_Location, D_Model, D_LOB, and D_Calendar

> _**Kindly note that the D_Calendar table was created using Data Analysis eXpressions (DAX) in Power BI Desktop. The DAX measures used are documented under the DAX section.**_


 ### _**FactSales Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/FactSales.png)


### _**D_Location Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Location.png)


### _**D_Model Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Model.png)


### _**D_LOB Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_LOB.png)


### _**D_Calendar Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Calendar.png)
---

### **Data Modeling**
This shows the relationship between the _**Fact Table**_ and _**Dimension Tables**_. Many-to-One(*:1) cardinality(relationship) was used.
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/e3f7fe36c478c40d8d45183bd9bcc8703053ecfc/Data%20Modeling.png)

You may ask, why can’t I just build my report on the single flat file? __**Why is Data Modeling important?**__ Below is why **Data Modeling** is essential:
- Improves report performance
- Simplifies DAX measures
- Reduces data redundancy
- Scales easily as data volume grows
---

## **Data Analysis eXpression(DAX)**
### **Anchor Measures** - These measures represent core aggregations used throughout the report.
**Total Revenue** - Calculates total sales revenue.
```DAX
Total Revenue = SUM ( FactSales[Revenue] )
```
**Total Units Sold** - Returns the units sold.
```DAX
Total Units Sold = SUM ( FactSales[Units Sold] )
```
**Average Revenue** - Calculates the average revenue value across sales transactions.
```DAX
Average Revenue = AVERAGE ( FactSales[Revenue] )
```
**Count of LOB** - Counts the number of distinct Lines of Business.
```DAX
Count of LOB = DISTINCTCOUNT ( D_LOB[Line Of Business] )
```
**Count of Store** - Returns the number of distinct stores.
```DAX
Count of Store = DISTINCTCOUNT ( D_Location[Store] )
```

### **Time Intelligence Measures** - These measures enable period-over-period comparison using the D_Calendar dimension.
**Revenue PM** - Returns total revenue for the previous month based on date context.
```DAX
Revenue PM =
CALCULATE (
    [Total Revenue],
    DATEADD ( D_Calendar[Date], -1, MONTH )
)
```
**Units Sold PM** - Returns total units sold for the previous month.
```DAX
Units Sold PM =
CALCULATE (
    [Total Units Sold],
    DATEADD ( D_Calendar[Date], -1, MONTH )
)
```

### **Variance Measures** - These measures calculate month-over-month (MoM) performance changes.
**Revenue MoM%** - Calculates the percentage change in revenue compared to the previous month.
```DAX
Revenue MoM % =
IF (
    AND ( [Total Revenue], [Revenue PM] ),
    DIVIDE ( [Total Revenue] - [Revenue PM], [Revenue PM], " " )
)
```
**Units Sold MoM%** - Calculates the percentage change in units sold compared to the previous month.
```DAX
Units Sold MoM % =
IF (
    AND ( [Total Units Sold], [Units Sold PM] ),
    DIVIDE ( [Total Units Sold] - [Units Sold PM], [Units Sold PM], " " )
)
```
---
## **Data Visualization**
### **Key KPIs (Cards)**
The following KPIs provide an instant snapshot of overall performance:
| KPI                     | Description                  |
| ----------------------- | ---------------------------- |
| **Total Revenue**       | ₦77.08bn total sales revenue |
| **LOB Count**           | 4 active Lines of Business   |
| **Store Count**         | 132 operational stores       |
| **Total Quantity Sold** | 830,000 units sold           |

### **Breakdown of other visuals**
1. **Revenue Contribution by Line of Business**
**Visual Type**: Treemap
**Purpose**: Shows how total revenue is distributed across different Lines of Business.
**Insights:**
- One Line of Business contributes ~71% of total revenue, indicating strong dependence on a single business line.
- Copier Sales and Parts contribute roughly 10% each, while Printer Sales have the smallest share.

2. **Region by Total Revenue**
**Visual Type**: Bar Chart
**Purpose**: Compares revenue performance across regions.
**Insights:**
- North East leads with ₦19.7bn in revenue.
- South West and South South follow closely.
- North Central records the lowest revenue contribution.

3. **Model by Total Units Sold**
**Visual Type**: Column Chart
**Purpose**: Highlights models driving sales volume.
**Insights:**
- Models 3002C and 3002P are the highest-selling products by unit count.

4. **Top 5 Stores by Average Revenue**
**Visual Type**: Bar Chart
**Purpose**: Identifies the most profitable stores based on average revenue.
**Insights:**
- Ankpa is the top-performing store with $5.8M average revenue.
- Other strong performers include Arochukwu, Ajaokuta, and Ekiti South-West.

5. **MoM % Change in Revenue and Units Sold**
**Visual Type**: Line Chart
**Purpose**: Tracks month-over-month percentage change for revenue and units sold.
**Insights:**
- Both revenue and units sold follow similar trends, indicating strong correlation.
- A significant decline in August suggests seasonality or operational challenges.
- Performance rebounds strongly in September and October.
---
## **Filters & Interactivity**
- Year slicers (2014, 2015)
- Month slicers (Jan–Dec)
These filters allow users to dynamically interact with the report.
---
## **Key Business Insights**
- Revenue is heavily concentrated in one Line of Business.
- Certain regions and stores significantly outperform others.
- Sales are driven by a small number of high-performing models.
- There is clear seasonal behavior, with a sharp decline in August.
- Sales recovery in later months indicates potential for forecast-based planning.
---
## **Tools & Skills Demonstrated**
- Power BI Desktop
- Power BI Service - cloud version of Power BI
- Power Query for Data Preparation
- Data Modeling
- Data Analysis eXpression(DAX)
- Business Analytics & Storytelling
---
_**To interact with the report, click [here](https://app.powerbi.com/view?r=eyJrIjoiMWFlZjM2NmYtNjJlYi00NjdlLWE1ZTMtYmJjMjQyYzFlODk0IiwidCI6IjVkNzU0ZDZhLTAxNWUtNGQ3ZS1hYjc1LTAwNmJlZGViZGVhMyJ9)**_
---
**Thank you for reading 🙏. If you have any question, you can reach out to me through my social media platforms below:**
[LinkedIn](https://www.linkedin.com/in/oluwapelumiarowosaye)
[Twitter](https://x.com/Pelumi_Analyst)

**Another version of the report👇**
![](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/33699ff871c301cfac98ce07eadc0ba571dd111c/Another%20Version%20-%20Sales%20Analysis%20Report%20-%20Power%20BI%20Project.png)
