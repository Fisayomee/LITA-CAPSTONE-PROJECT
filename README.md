# LITA-CAPSTONE-PROJECT SALES DATA
This is where I documented my first project while learning Data Analysis with the Incubator Hub

## PROJECT TITLE: SALES DATA
This project deals with analyzing the sales performance of a retail store.This dataset captures transactional sales data, providing a detailed view of customer orders, including product, region, and revenue information. It involves analyzing sales trends, regional performance, enabling insights into the drivers of revenue and high-demand products. The goal is to produce an interactive Power BI dashboard that highlights these findings.
### Data Description
The dataset includes the following field:
- OrderID: A unique identifier for each order.
- CustomerId: A unique identifier for each customer placing an order.
- Product: The specific product purchased in each transaction.
- Region: The geographical location (e.g., North, South, East, West) where the order was placed.
- OrderDate: The date when the order was made.
- Quantity: The number of units purchased for each product in an order.
- UnitPrice: The price per unit of the product.
- Total Sales: The total sales value for the order, calculated as Quantity * UnitPrice

### Tools used

- Microsoft excel - For Data Cleaning, Analysis and Visualisation
- Structured Query Language - For querying data
- Power BI - For Data Visualisation and Report

### Basic Statistics about Dataset
- Total Sales: 2.1 Million
- Average Sales: 211.8
- Total Customer: 9921
- Total Quantity: 68.5K

### Exploratory Data Analysis
EDA involved the exploratory of the Data to answer some questions about the data;

1. Retrieve the total sales for each product category.
2. Find the number of sales transactions in each region.
3. Find the highest-selling product by total sales value.
4. Calculate total revenue per product.
5. Calculate monthly sales totals for the current year.
6. Find the top 5 customers by total purchase amount.
7. Calculate the percentage of total sales contributed by each region.
8. Identify products with no sales in the last quarter.
### DATA ANALYSIS
#### Excel
- Perform an initial exploration of the sales data. Use pivot tables to summarize total sales by product, region, and month.
- Use Excel formulas to calculate metrics such as average sales per product and total revenue by region.
- Create any other interesting report
 ![Excel Sales data](https://github.com/user-attachments/assets/37609006-3b0c-4a44-90c4-e49140acf433)

PIVOT TABLE
- REGION BY REVENUE
![REGION BY REVENUE](https://github.com/user-attachments/assets/67f58d67-5de1-4207-9fd8-27f29a75a6f6)

- PRODUCT BY REVENUE
![PRODUCT BY REVENUE](https://github.com/user-attachments/assets/0ae4a8a7-81e5-4bb9-9cc0-03eff6e6228d)

- MONTHLY REVENUE
![MONTHLY REVENUE](https://github.com/user-attachments/assets/28d3e321-095d-498e-9d12-75cacca190cf)

#### SQL
1. Retrieve the total sales for each product category.
  ```
select product, sum (total_revenue) as TotalSales from SalesData
Group by Product
```

2. Find the number of sales transactions in each region.
```
Select region, count (*) as NumberofTransacton from SalesData
Group by Region
```

3. Find the highest-selling product by total sales value.
```
select top 1 product, sum(total_revenue) as TotalSales from Salesdata
group by product
```

4. Calculate total revenue per product.
```
Select product, sum(Quantity*unitprice) as Totalrevenue from SalesData
group by Product
```
5. Calculate monthly sales totals for the current year.
```
Select month(Orderdate), sum(Total_Revenue) as MonthlySales from SalesData
Where year(Orderdate)= year('2024')
Group by month(Orderdate)
Order by month(OrderDate)
```
6. Find the top 5 customers by total purchase amount.
```
SELECT TOP 5 CUSTOMER_ID, SUM(TOTAL_REVENUE) AS TOTALPURCHASEAMOUNT FROM SALESDATA
GROUP BY CUSTOMER_ID
ORDER BY 2 DESC
```
7. Calculate the percentage of total sales contributed by each region.
```
SELECT REGION, SUM(TOTAL_REVENUE) AS REGIONTOTALSALES,
FORMAT(ROUND((SUM (TOTAL_REVENUE) / CAST((SELECT SUM(TOTAL_REVENUE) FROM SalesData) as Decimal(10,2))* 100),1),'0.#')
as PERCENTAGEOF
FROM SALESDATA
GROUP BY REGION
```
8. Identify products with no sales in the last quarter.
```
Select product from SalesData
Group by Product
Having sum (CASE
               WHEN OrderDate between '2024-06-01' and '2024-08-31'  then 1
			   ELSE 0
			   END) =0
```





