# LITA_CAPSTONE_PROJECT
Here, I documented my final project while learning Data Analysis with the Incubator Hub.

## Project Title: Sales Data Analysis

### Table_of_content
[Project Overview](#project-overview)

[Data Source](data-source)

[Tools Used](tools-used)

[Data Cleaning and Preparation](data-cleaning-and-preparation)

[Project Structure](project-structure)

[Exploratory Data Analysis](exploratory-data-analysis)

[Data Analysis](data-analysis)

[Data Visualization](data-visualization)

[Recommendations](recommendations)


## Project Overview
---
This Data Analysis project aims to generate insights into the sales performance of certain products in the years 2023 and 2024. By analyzing the variuos parameters presented in the document file, I have gathered some insights to help the company involved to have a general overview of how well their products performed in the market. I have also used the information obtained to tell compelling stories around the data presented. 


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

```SQL
CREATE DATABASE PROJECT_DB
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

SELECT Region, SUM(Revenue) AS RegionTotalSales,
FORMAT(ROUND((SUM(Revenue) / CAST((SELECT SUM(Revenue) FROM[dbo].[LITA Capstone Dataset_SalesData] ) AS DECIMAL(10,2)) * 100), 1), '0.#') 
AS PercentageOfTotalSales
FROM [dbo].[LITA Capstone Dataset_SalesData]
GROUP BY Region
ORDER BY PercentageOfTotalSales DESC

---products with no sales in the last quarter---
Select product, sum(quantity) AS Sales
from [dbo].[LITA Capstone Dataset_SalesData]
where month(OrderDate) between 10 and 12----months 10, 11, 12 (October, November, December)
Group by Product
having sum(quantity)=0
```


4. Power BI
I created visuals, measures and new columns

### Data Visualization
- Microsoft Excel

![Capstone Sales_1](https://github.com/user-attachments/assets/51ffe030-cbf8-4250-98e9-2aa75d69875b)

![Capstone Sales_2](https://github.com/user-attachments/assets/b480ccda-353b-42eb-b8c4-171fdbb815b5)

![Capstone Sales_11](https://github.com/user-attachments/assets/e16078ae-59b9-4bcc-a98f-a3ea40a9bb33)

![Capstone Sales_12](https://github.com/user-attachments/assets/d480c9ec-a2da-4c18-b55b-a8ebabd8bdba)


-Power BI 

![Capstone Sales_3](https://github.com/user-attachments/assets/5e0f60a8-2650-4ea4-b9d8-d492a415623e)

![Capstone Sales_4](https://github.com/user-attachments/assets/d7cebd27-306d-4024-a06d-e1e406b8c43d)

![Capstone Sales_5](https://github.com/user-attachments/assets/fe9f512b-9111-4775-9b7e-b1d359b966b8)

![Capstone Sales_6](https://github.com/user-attachments/assets/cb462d37-58db-450d-a7e5-cd9f1e639a90)

![Capstone Sales_7](https://github.com/user-attachments/assets/b815819d-e4c7-47c3-90e7-f120e8da99d8)

![Capstone Sales_8](https://github.com/user-attachments/assets/79402057-ece3-4950-99ca-ee3a131ae659)

![Capstone Sales_9](https://github.com/user-attachments/assets/264ba349-77e1-4c93-ac98-c62bffd5b200)

![Capstone Sales_10](https://github.com/user-attachments/assets/b1e2e053-f019-4909-bc76-95c9afe4c4f4)

### Recommendations
Based on the information obtained from this analysis, the product with the highest sales  was Hats, while Jackets had the lowest sale generated. Hence, the company may focus more on the advertisement and publicity for Jackets and other products with low sales turnout. The Month with the highest sales was Februaray: this may have been as a result of the fact that Valentine's day is celebrated in February which is an avenue for gifts buying and giving. Therefore, the company may ensure that enough products are made available in February to meet the demands. The Product with the highest revenue was shoes, indicating a strong point for the company. In addition, the South recorded the highest revenue and sales, sugesting that more attention should be paid to the other regions, so as to also boost their sales. 
The top 5 customers by total purchase amount were Cus1431, Cus1249, Cus1302, Cus1115, Cus1005. Incentives like discounts and free delivery services may be given to these customers to show appreciation for their purchase and encourage subsequent purchases.  
