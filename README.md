# LITA_CAPSTONE_PROJECT
Here, I documented my final project while learning Data Analysis with the Incubator Hub.

## Project Title: Sales Data Analysis
## Project Overview
---
This Data Analysis project aims to generate insights into the sales performance of certain products in the years 2023 and 2024. By analyzing the variuos parameters presented in the document file, I have gathered some insights to help the company involved to have a general overview of how well their products performed in the market. I have also used the information obtained to tell compelling stories around the data presented. 

### Table_of_content
#### Data Sources
#### Tools Used
#### Data Cleaning and Preparation
#### Project Structure
#### Exploratory Data Analysis
#### Data Analysis
#### Data Visualization
#### Recommendations
#### Conclusions

### Data Source
---
The data was obtained from the Learning Managagement System (LMS) Canvas platform set up by the organizers, the Incubator Hub. LITA Capstone Dataset; SalesData.  

### Tools Used
---
For this project, I made use of three different softwares; Microsoft Excel [Download Here](https://www.microsoft.com), Microsoft SQL, and Microsoft PowerBI; all of which can be obtained from the Microsoft Store.
- Microsoft Excel was used for data cleaning, analysis, and visualization
- SQL-Structured Query Language for querying of data 
- Power BI for analysis and visualization.
- GitHub for portfolio building

### Data Cleaning and Preparation
---
After the file was obtained, I performed the following actions;
- Data loading and inspection
- Removal of duplicates
- Data formatting

### Exploratory Data AnalysiS
---
Exploratory data analysis invlolved exploring the data to answer some questions about the data such as; 
- The product, region, and months with the highest sales
- The product, region, and months with the highest revenue
- Average sales per product

### Data Analysis
---
1. Microsoft Excel
In Microsoft Excel, a revenue column was created, which was calculated as Unit Price*Quantity, while Total Sales was obtained as Total Sales = Total Quantity Sold = Unit sold.
After which Pivot table was used to summarise the data, and excel funtions used to calculate average sales per product and total revenue by region.
2. SQL
   Queries were generated in SQL to carry out some calculations and analysis.
   
  ```CREATE DATABASE PROJECT_DB
---FOR SALES DATA---

select * from [dbo].[LITA Capstone Dataset_SalesData]

---total sales for each product category---
select product, sum (quantity) as sales_per_product from [dbo].[LITA Capstone Dataset_SalesData]
group by product

--number of sales transaction in each region---
select region, sum(quantity) as sales_per_region from [LITA Capstone Dataset_SalesData]
group by Region

---highest-selling product by total sales value---
select product, sum(quantity*UnitPrice) as total_sales from [LITA Capstone Dataset_SalesData]
group by product
order by total_sales desc

---total revenue per product---
select product, sum(revenue)as total_revenue_per_product from [LITA Capstone Dataset_SalesData]
group by Product

--to create a column for ordermonth--
Alter table [dbo].[LITA Capstone Dataset_SalesData]
ADD OrderMonth nvarchar(50)

update [dbo].[LITA Capstone Dataset_SalesData]
set OrderMonth=datename(month,orderdate)

--to create a column for OrderYear--
Alter table [dbo].[LITA Capstone Dataset_SalesData]
ADD OrderYear int

update [dbo].[LITA Capstone Dataset_SalesData]
set OrderYear=Year(OrderDate)

---monthly sales totals for the current year (2024)---
Select OrderMonth, sum(quantity) AS TotalSales
from [dbo].[LITA Capstone Dataset_SalesData]
where OrderYear=2024
GROUP BY OrderMonth

---top 5 customers by total purchase amount--
Select top 5
Customer_Id, sum(revenue) AS TotalPurchase
from [dbo].[LITA Capstone Dataset_SalesData]
group by Customer_Id

--- percentage of total sales contributed by each region---

Select Region, sum(revenue)/sum(quantity)*0.1 AS Percentage_of_total_sales
from [dbo].[LITA Capstone Dataset_SalesData]
Group by Region
order by Percentage_of_total_sales

---products with no sales in the last quarter---
Select product, sum(quantity) AS Sales
from [dbo].[LITA Capstone Dataset_SalesData]
where month(OrderDate) between 10 and 12----months 10, 11, 12 (October, November, December)
Group by Product
having sum(quantity)=0```


3. Power BI
I created visuals, measures and new columns. 

### Data Visualization



