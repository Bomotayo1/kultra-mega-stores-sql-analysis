# kultra Mega Stores: SQL Sales Analysis

## Overview
This project features a detailed analysis of four years' worth of sales and order data from Kultra Mega Stores Analysis. Using SQL, the project uncovers key business insights, including top-performing products, customer behaviors, shipping cost efficiency, and regional sales performance. The analysis supports strategic decision-making aimed at improving profitability, optimizing shipping logistics, and strengthening customer engagement across various segments.

## Business Questions 
1. Which product category had the highest sales?
2. What are the Top 3 and Bottom 3 regions in terms of sales?
3. What were the total sales of appliances in Ontario?
4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
5. KMS incurred the most shipping cost using which shipping method?
6. Who are the most valuable customers, and what products or services do they typically purchase?
7. Which small business customer had the highest sales?
8. Which corporate customer placed the most number of orders in 2009-2012?
9. Which consumer customer was the most profitable one?
10. Which customer returned items, and what segment do they belong to?
11. If the delivery truck is the most economical but the slowest shipping method, and express air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the order priority? Explain your answer

## Tools
[SQL Server Management Studio](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)

## Approach
I imported the data into SQL Server Management Studio using the flat file option. Afterward, I selected the top 10 rows to review all the columns. Once I confirmed the structure, I began writing queries to explore the data and answer my business questions.

## Sample Query
1. Which Product Category had the highest sales?
   ```sql
   select top 1 product_category, sum(sales) AS [Total sales]
   FROM   dbo.[KMS Sql Case Study]
   GROUP BY  product_category
   ORDER BY   [Total sales] desc
<img width="269" height="57" alt="Screenshot 2026-09-21 123924" src="https://github.com/user-attachments/assets/774a8d98-a44c-4923-a0e7-6e32e8990522" />

2. What are the Top 3 and Bottom 3 regions in terms of sales?
   
   ---**TOP 3 Regions**
 ```sql
    select top 3 Region, sum(sales) AS [Total sales]
     from   dbo.[KMS Sql Case Study]
     group by  region
     order by  [Total sales] desc
```
  <img width="183" height="91" alt="Screenshot 2026-09-21 124636" src="https://github.com/user-attachments/assets/e682bd59-2f2e-4591-be94-8c1cd466f958" />

  ---- **Bottom 3 regions**
```sql
        Select top 3 Region, sum(sales) AS [Total sales] 
        From  dbo.[KMS Sql Case Study]
        group by region
        Order by  [Total sales] Asc
```
<img width="263" height="91" alt="Screenshot 2026-09-21 132529" src="https://github.com/user-attachments/assets/d9d9c645-6b75-4da9-a0b2-be5890425b95" />

3. What were the total sales of appliances in Ontario?
   ```sql
          SELECT PRODUCT_SUB_CATEGORY ,REGION, SUM(SALES) AS [TOTAL SALES]
           FROM dbo.[KMS Sql Case Study]
           WHERE PRODUCT_SUB_CATEGORY = 'APPLIANCES'
          AND REGION = 'ONTARIO'
          GROUP BY PRODUCT_SUB_CATEGORY, REGION
          ORDER BY [TOTAL SALES]
 <img width="329" height="47" alt="Screenshot 2026-09-21 132756" src="https://github.com/user-attachments/assets/b51637bf-3772-42f5-be83-9a478530d351" />

4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers?
    ```sql
        select top 10 Customer_Name,customer_segment, sum(sales) AS [Total sales], sum(profit) AS [Total profit],
         count(distinct Order_ID) AS num_orders,
         Avg(CAST(discount as float)) as Avg_discount
          from dbo.[KMS Sql Case Study]
          group by Customer_Name,Customer_Segment
           order by [Total sales] ASC
<img width="533" height="210" alt="Screenshot 2026-09-21 133332" src="https://github.com/user-attachments/assets/c51a608c-2fc3-4adf-9fb5-9981f676600b" />

5. Most costly Shipping method
   ```sql
   SELECT TOP 1 SHIP_MODE, SUM(SHIPPING_COST) AS [TOTAL SHIPPING COST]
   FROM dbo.[KMS Sql Case Study]
   GROUP BY SHIP_MODE
   ORDER BY [TOTAL SHIPPING COST]DESC
<img width="243" height="49" alt="Screenshot 2026-09-21 133748" src="https://github.com/user-attachments/assets/fe060334-f544-494c-8757-37dad573cd00" />

6. Who are the most valuable customers, and what products or services do they typically purchase?
   ```sql
   SELECT top 5 CUSTOMER_NAME, PRODUCT_NAME, SUM(SALES) AS [TOTAL SALES], sum(profit) As [Total Profit],
    count(Distinct Order_ID) AS num_orders,
       SUM(sales) / Count(Distinct Order_ID) AS avg_Order_value
          FROM dbo.[KMS Sql Case Study]
             GROUP BY Customer_Name, Product_Name
                ORDER BY [TOTAL SALES]DESC
  <img width="760" height="142" alt="Screenshot 2026-09-21 134221" src="https://github.com/user-attachments/assets/22a104a1-a478-4499-b6b6-d0c2c1a0310f" />

7. Which small business customer had the highest sales?
     ```sql
            SELECT TOP 1 Customer_Name, Customer_Segment, SUM(SALES) AS [TOTAL SALES]
            FROM dbo.[KMS Sql Case Study]
             WHERE [Customer_Segment] = 'SMALL BUSINESS'
             GROUP BY Customer_Name, Customer_Segment
              ORDER BY [TOTAL SALES]DESc
 <img width="343" height="48" alt="Screenshot 2026-09-21 134518" src="https://github.com/user-attachments/assets/de48e5b2-efb8-49c9-99f3-4aeb0595c45a" />

8.  Which corporate customer placed the most number of orders in 2009-2012?
      ```sql
      select top 1 customer_Name, Count(distinct Order_ID) AS num_Orders
         from dbo.[KMS Sql Case Study]
          where customer_segment = 'Corporate'
          And year(Order_Date) between 2009 and 2012
          Group By Customer_Name
           Order By num_Orders DESC
   <img width="221" height="52" alt="Screenshot 2026-09-21 134846" src="https://github.com/user-attachments/assets/859dabd4-494b-49e7-8bd4-48db3396416c" />

9. Which consumer customer was the most profitable one?
     ```sql
         select top 1 customer_Name, sum(Profit) as TotalProfit
          from dbo.[KMS Sql Case Study]
           where customer_segment = 'Consumer'
           Group by customer_Name
           Order by Totalprofit Desc
  <img width="197" height="45" alt="Screenshot 2026-09-21 135117" src="https://github.com/user-attachments/assets/e8a7e307-f8f3-4587-90ae-3d99f67c00d7" />

10. Which customer returned items, and what segment do they belong to?

11. If the delivery truck is the most economical but the slowest shipping method, and express air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the order priority? Explain your answer
    ```sql
    select 
      order_priority, ship_mode,
	  count(*) AS num_orders,
	  sum(shipping_cost) AS total_cost
      from dbo.[KMS Sql Case Study]
    where  
       (Order_priority IN ('Low','Medium') AND ship_mode = 'Express Air')
	     OR (Order_priority IN ('Critical''High') And Ship_mode = 'Delivery Truck')
	   Group by order_priority, ship_mode
	     order by total_cost DESC
 <img width="328" height="66" alt="Screenshot 2026-09-21 135621" src="https://github.com/user-attachments/assets/3d82f892-88a3-4d60-8976-bad2c934d7a3" />
