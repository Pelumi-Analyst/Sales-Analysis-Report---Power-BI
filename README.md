# Sales Analysis Report
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/95a7eec2120786b8905adfdb858c6c9c55670555/Sales%20Analysis%20Report%20-%20Power%20BI%20Project.png)
---
**Report Page Overview**
---
This report page provides a high-level sales performance analysis, focusing on revenue, units sold, regional performance, models, and store performance. It is designed to help business leaders and sales managers quickly understand where revenue is coming from, which regions and stores are performing best, and how sales are trending over time.
---
**Business Questions Answered**
---
- What is the total revenue?
- What is the total units sold?
- Which regions contribute the most revenue?
- Which models drive unit sales?
- What are the top-performing stores by average revenue?
- How is revenue distributed across Lines of Business (LOB)?
- How does revenue and units sold change month-over-month (MoM)?
---
**Data Preparation & Data Modeling**
---
The dataset used was a single flat file(Denormalized table) containing transactional sales data with columns such as Region, Market, Store, Model, Line of business, Trade Date, Revenue, and Units Sold.

To improve performance, readability, and analytical flexibility, the data was **normalized into a star schema** consisting of one Fact Table and four Dimension Tables.

_**Fact Table**_ - FactSales

_**Dimension Tables**_ - D_Location, D_Model, D_LOB, and D_Calendar

> _**Kindly note that the D_Calendar table was created using Data Analysis eXpressions (DAX) in Power BI Desktop. The DAX measures used are documented under the DAX section.**_


 _**FactSales Table**_
![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/FactSales.png)


_**D_Location Table**_

![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Location.png)


_**D_Model Table**_

![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Model.png)


_**D_LOB Table**_

![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_LOB.png)


_**D_Calendar Table**_

![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/26b4c6ac0e8283c517e07e736a0cf4b9df1aa043/D_Calendar.png)
---

_**Data Modeling**_

![image alt](https://github.com/Pelumi-Analyst/Sales-Analysis-Report---Power-BI/blob/e3f7fe36c478c40d8d45183bd9bcc8703053ecfc/Data%20Modeling.png)
