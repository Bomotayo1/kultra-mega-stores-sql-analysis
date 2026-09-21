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

