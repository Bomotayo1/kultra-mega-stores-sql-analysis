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

 The bottom 10 customers by total sales were identified, along with their total profit, number of orders placed, and average discount received. This additional detail was included specifically to understand not just who these customers are, but why they ended up at the bottom of the revenue list, since the appropriate advice depends heavily on the underlying cause.
 
  The most immediately apparent pattern across all ten customers is the extremely low number of orders placed. Every customer in this group placed only one, two, or, in one case, four orders in total. This is an important distinction to make before offering any advice, because it changes the nature of the problem entirely. These are not customers who shop frequently but spend small amounts each time — they are customers who have barely engaged with KMS at all. This means the appropriate strategy is centered on re-engagement and encouraging repeat business, rather than trying to increase the size of each order.
  
  ## Recommendations for Management

Address the unprofitable customers first, before attempting to grow their business. For Michelle Ellison, Nicole Fjeld, Katrina Edelman, and Eric Murdock, increasing their order volume without first understanding why their existing orders are unprofitable would only increase the company's losses. Management should investigate whether these losses stem from high shipping costs relative to order value or from low-margin products, and correct that underlying issue before pursuing any growth strategy with these specific customers.

Focus on re-engagement rather than upselling for the group as a whole. Since nearly all ten customers have purchased only once or twice, the most effective lever for increasing revenue from this group is encouraging them to return for a second, third, or fourth purchase, rather than trying to convince them to spend more within a single order. Outreach such as personalized follow-up communication after a first purchase, a small loyalty incentive for a repeat order, or a simple "we'd love to see you again" promotion would likely be more effective than a strategy aimed at increasing basket size.

Determine whether these customers are new or long-standing but stagnant. A customer who has only purchased once because they are new should be treated differently from a customer who has been with KMS for years but has never grown beyond one or two purchases. The former simply needs time and nurturing, while the latter represents a genuine warning sign that something about their experience with KMS has not encouraged continued business, and may warrant a direct check-in from a sales or account representative.

Compare product exposure between these customers and KMS's best customers. It is possible that these bottom 10 customers have never been exposed to the product categories that drive the most value for KMS's top customers. Reviewing what these customers have purchased against what high-value customers typically buy could reveal specific product categories or items that should be recommended or promoted to this group.

Recognize that this group spans multiple customer segments, so a single approach will not fit everyone. The bottom 10 includes Small Business, Corporate, Consumer, and Home Office customers in roughly equal measure. This suggests the issue is not isolated to one segment, and outreach should be tailored accordingly, for example, a Corporate customer may respond better to a dedicated account manager reaching out personally, while a Consumer customer may respond better to a straightforward promotional email.

5. Most costly Shipping method
   ```sql
   SELECT TOP 1 SHIP_MODE, SUM(SHIPPING_COST) AS [TOTAL SHIPPING COST]
   FROM dbo.[KMS Sql Case Study]
   GROUP BY SHIP_MODE
   ORDER BY [TOTAL SHIPPING COST]DESC
<img width="243" height="49" alt="Screenshot 2026-09-21 133748" src="https://github.com/user-attachments/assets/fe060334-f544-494c-8757-37dad573cd00" />

 The results showed that Delivery Truck accounted for the highest total shipping cost of all three methods, at approximately $51,972. This was higher than Regular Air, which totaled around $48,018, and far higher than Express Air, which totaled only about $7,851.
 
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
    SELECT 
    Ship_mode,
    Order_priority,
    COUNT(*) AS num_shipments,
      AVG(shipping_cost) AS avg_cost,
      SUM(shipping_cost) AS total_cost
      FROM dbo.[KMS Sql Case Study]
      GROUP BY Ship_mode, Order_priority
     ORDER BY Ship_mode, Order_priority;
 <img width="536" height="351" alt="Screenshot 2026-09-21 144128" src="https://github.com/user-attachments/assets/45de8550-ce44-4263-a062-e82126a50d1c" />

This question directly tested the common assumption stated at the outset, that Delivery Truck is the cheap, slow shipping method, while Express Air is the fast, expensive one. This assumption was examined from three separate angles before concluding.

First, average cost per shipment was compared across all three methods, rather than looking at total cost alone, since total cost can be misleading when volume differs between methods. This comparison showed that Regular Air averaged about $7.66 per shipment, Express Air averaged about $7.99 per shipment, and Delivery Truck averaged about $45.35 per shipment. This is a striking result: Delivery Truck cost nearly six times more per shipment than either air-based method. If the original assumption were accurate, Truck should have shown the lowest average cost of the three, not the highest.

Second, to rule out the possibility that Truck's higher cost was simply a byproduct of carrying larger or heavier goods (such as furniture), average cost was examined within individual product categories rather than across the dataset as a whole. This comparison showed that even for a light, non-bulky category like Office Supplies, Delivery Truck cost about $53.94 per shipment on average, compared to only about $7.29 for the same category shipped via Express Air. The same pattern of Truck being the most expensive option held true across every product category examined, including Furniture and Technology. This ruled out the theory that Truck's cost was simply a reflection of shipping bulkier items; the method was consistently more expensive regardless of what was actually being shipped.

Third, the findings from the priority-based analysis were considered further supporting evidence. Since Delivery Truck usage was spread evenly across all priority levels rather than concentrated among low-priority, non-urgent orders, there was no indication that its high cost was being offset or justified by strategic, priority-based use. It was not being reserved selectively for situations where its slower speed would be an acceptable tradeoff.

Taken together, these three angles of investigation each independently reached the same conclusion: Delivery Truck is not functioning as the economical shipping option it is commonly assumed to be. It is, in fact, the most expensive method per shipment across every product category, and its use shows no relationship to order urgency. This means the original premise embedded in the business question does not hold true for KMS's actual data.

## Overall Conclusion

The three findings build directly on one another. The first finding, that Delivery Truck had the highest total shipping cost despite being used far less often than Regular Air served as the initial signal that something was inconsistent with the assumption that Truck is the "cheap" shipping method. The second finding confirmed that shipping method selection is not connected to order priority, since Delivery Truck appeared in roughly equal proportions across every urgency level. The third finding then confirmed, through multiple angles of testing, that Delivery Truck is genuinely the most expensive shipping method on a per-shipment basis, not merely expensive due to volume, product type, or any other confounding factor.

Based on this evidence, it can be concluded that KMS did not appropriately allocate shipping costs based on order priority. More significantly, the inefficiency is not limited to priority mismatches alone, the company appears to be relying heavily on a shipping method that is both slow and the most costly option available, with no clear justification tied to cost-saving or urgency. This points to a broader operational issue in how shipping methods are selected, independent of how urgent any individual order happens to be.

feel free to connect with me on [linkedin](www.linkedin.com/in/omotayo-babatunde) or send an email to [bomotayo99@gmail.com](mailto:bomotayo99@gmail.com)
   
