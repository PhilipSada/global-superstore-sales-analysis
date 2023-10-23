# Global Super Store: Sales Analysis
## Project Overview
This is a SQL and Tableau project on the sales analysis of a global superstore. This project aims to provide insights to answer important questions and help the superstore make data driven decisions.
The dataset used in this project can be found in Kaggle.

You can interact with the dashboard in tableau public [here](https://public.tableau.com/views/SalesDashboard2GlobalSuperstore_16978357780940/SalesDashboard3?:language=en-US&:display_count=n&:origin=viz_share_link)

![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/742c681b-523b-4cf3-921e-31960cb6702d)



## Problem Statement
1. Which product generates the most overall sales?
2. Which markets are  our top selling markets?
3. Which country in each of those markets has the highest overall sales?
   
## Exploratory Data Analysis
The following explorary data analysis was conducted in Microsoft SQL Server to understand the dataset.

The query below was executed to find out the number of items in the data
```sql
select count(*) from [dbo].[Orders$]
```
The query below was executed to check if the Order ID can be a primary key. The result showed that order id can't be a primary key alone since multiple rows have the same order id
```sql
select [Order ID], count(*) from [dbo].[Orders$] group by [Order ID] having count(*) > 1
```
The query below was executed to check if Order Date is less than Ship Date. The result showed that all the order dates were less than the ship dates.
```sql
select * from [dbo].[Orders$] where [Ship Date] < [Order Date]
```
The query below was executed to find the distinct ship modes in the data. The result showed that there are 4 distinct ship modes (First Class, Same Day, Standard Class and Second Class)
```sql
select distinct [Ship Mode] from [dbo].[Orders$]
```
The query below was executed to find the time range( min and max days) for the ship modes(i.e Ship Mode = 'Second Class')
```sql
select min(a.NumOfDays) MinDays, max(a.NumOfDays) MaxDays from (
select DATEDIFF(DAY, [Order Date], [Ship Date]) as NumOfDays, * from [dbo].[Orders$] where [Ship Mode] = 'Second Class'
) a
```
The query below was executed to check if the customer can order multiple items. The result showed that a customer can order multiple times
```sql
select min(a.NumOfDays) MinDays, max(a.NumOfDays) MaxDays from (
select DATEDIFF(DAY, [Order Date], [Ship Date]) as NumOfDays, * from [dbo].[Orders$] where [Ship Mode] = 'Second Class'
) a
```

## Data Analysis and Visuals
Tableau was used to conduct the sales analysis and answer the problem statement. The following Tableau features were some of the features incorporated for this project:
- Filters
- Tooltips
- Dashboard Actions (Go to URL, Filter)

![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/bc682b86-62db-4158-8f74-0e4a7b1bdcad)
![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/849df239-6971-4d12-ba6c-ff5674dd3531)

![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/aadd314b-37c6-4e01-bb54-11a81444a085)
![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/7d0a5861-b221-44f7-b92e-e30ce28a7b41)
![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/51270453-82fa-4028-8860-ec4b6b18049d)
![Dashboard](https://github.com/PhilipSada/global-superstore-sales-analysis/assets/55988995/8f0bfdcf-e6d6-40a4-9ccd-78a2d1aba1be)

1. From the dashboard, phones generated the most overall sales with a figure of 1,706,824
2. From the dashboard, the top 4 markets of the global superstore are APAC, EU, US and LATAM with sales of 3,586K, 2,938K, 2,297K and 2,938K respectively.
3. From the dashboard, the country with the highest sales in the APAC market is Australia with sales of 270,487. Also, the country with the highest sales in the EU market is United Kingdom with sales of 485,171.
   Furthermore, the country with the highest sales in the US market is United States with sales of 457,688 and the country with the highest sales in the LATAM market is El Salvador with sales of 153,639
   
## Recommendations
Based on the analysis, the following are recommended:
- Since phones generated the highest sales figure compared to other products, the company should implement targeted strategies to capitalize on this success. For example, they could focus on strengthening product bundling by creating attractive packages that combine phones with complementary items like accessories, encouraging customers to make larger purchases.
-  Global Superstore could develop a targeted international marketing strategy for APAC, EU, US and LATAM markets. This could involve focusing on enhancing customer experience in these markets which can be achieved through localized customer support, addressing regional concerns promptly, and offering region-specific customer incentives

