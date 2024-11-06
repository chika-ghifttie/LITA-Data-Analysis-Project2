# Subscription-Analysis-Dashboard

## Project Overview

This project aims to analyze customer data from a subscription service to uncover insights into customer behavior, subscription patterns, and key trends in cancellations and renewals. The final deliverable is an interactive Power BI dashboard that presents these insights.


![Overview](https://github.com/user-attachments/assets/e0f6ac65-81b5-4b86-b548-80adfb7eabc1)




## Objectives

- Identify subscription patterns and key trends.
- Segment customers based on subscription behaviors.
- Visualize cancellations, renewals, and active subscriptions.

## Tools Used

- Excel: Data exploration and calculation of metrics.
- SQL: Querying data for deep insights.
- Power BI: Visualization of analysis results.

  ## Data Analysis Process
  
1. Excel Analysis
Goal: Analyze customer data for patterns and metrics.
Tasks:
Use pivot tables to summarize subscription patterns.


![Pivot Table for Subscription Count by Type](https://github.com/user-attachments/assets/477b1cf3-b396-42d2-a6c7-94bbde33e1db)


Calculate the average subscription duration.




![Average Subscription Duration Calculation](https://github.com/user-attachments/assets/a8c44515-6a7e-487d-a94a-c5b68b435dfc)




 - Cancelled Subscription.
 - Count of cancelled subscription by region


![Additionanal Report](https://github.com/user-attachments/assets/f9332658-56af-4c99-9010-e1afdb4813c7)


3. SQL Analysis

   
##### Queries to extract insights on subscription data.

- Retrieve the total number of customers by region.

```sql
Select * from [dbo].[Sheet3$]
SELECT Region,
COUNT(CustomerID)
AS TotalCustomers
FROM [dbo].[Sheet3$]
GROUP BY Region
ORDER BY TotalCustomers DESC
```


- Identify the most popular subscription type by customer count.

```sql
Select * from [dbo].[Sheet3$]
SELECT SubscriptionType,
COUNT(CustomerID) 
AS NumberOfCustomers
FROM [dbo].[Sheet3$]
GROUP BY SubscriptionType
ORDER BY NumberOfCustomers DESC
```
  
- Find customers who canceled within the first 6 months.

```sql
Select * from [dbo].[Sheet3$]
SELECT 
    CustomerID,
    SubscriptionStart,
    SubscriptionEnd,
    DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS SubscriptionDurationMonths
FROM [dbo].[Sheet3$]   
WHERE 
    DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) <= 6
    AND SubscriptionEnd IS NOT NULL;
```

- Calculate the average subscription duration.

```sql
Select * from [dbo].[Sheet3$]
SELECT AVG(AverageDuration)
AS AverageSubscriptionDuration
FROM [dbo].[Sheet3$]
```

- Find customers with subscriptions longer than 12 months.

```sql
Select * from [dbo].[Sheet3$]
SELECT CustomerID, SubscriptionStart, SubscriptionEnd, AverageDuration
FROM [dbo].[Sheet3$]
WHERE AverageDuration > 12;
```

- Calculate total revenue by subscription type.

```sql
Select * from [dbo].[Sheet3$]
SELECT SubscriptionType,
SUM(Revenue)
AS TotalRevenue
FROM [dbo].[Sheet3$]
GROUP BY SubscriptionType
ORDER BY TotalRevenue DESC;
```

- Identify the top 3 regions by cancellation count.

```sql
Select * from [dbo].[Sheet3$]
SELECT Top 3 Region,
COUNT(CustomerID) AS
CancellationCount
FROM [dbo].[Sheet3$]
WHERE Canceled = 0
GROUP BY Region
```
- Track the total number of active and canceled subscriptions.

```sql
Select * from [dbo].[Sheet3$]
SELECT 
    CASE 
        WHEN SubscriptionEnd IS NULL THEN 'Active'
        ELSE 'Canceled'
    END AS SubscriptionStatus,
    COUNT(*) AS TotalSubscriptions
FROM [dbo].[Sheet3$]
GROUP BY 
    CASE 
        WHEN SubscriptionEnd IS NULL THEN 'Active'
        ELSE 'Canceled'
    END;
```

- Calculate revenue by subscription type.
```sql
Select * from [dbo].[Sheet3$]
SELECT 
    SubscriptionType,
    SUM(Revenue) AS TotalRevenue
FROM [dbo].[Sheet3$]
GROUP BY 
    SubscriptionType;
```

5. Power BI Dashboard
   
This section analyzes and visualizes customer data, cancellation patterns, and subscription trends through interactive Power BI dashboards.
This provides insights into customer behavior, trends over time, and cancellation rates.

### Customer Segment

 To visualize customer trends and behavior, track total active customers, and measure customer attrition.

 #### Key Visualizations Used
 
- Slicers: Used for interactive analysis, including filters for Region, Subscription Type, and Customer ID.
  
- Card Visualization: Displayed important metrics such as the Total Number of Active Customers and The Customer Attrition Rate.
     - The Total Number of Active Customers is 11.
     -  The Customer Attrition Rate is 4500%
  
- Table Visualization: Displays the Top 10 Customers based on the most relevant criteria like Subscription Revenue.
   The table includes the following columns:
  - Customer Name
  - Subscription Type
  - Region
 
- Bar Chart Visualization:

    - Count of CustomerIDs by Subscription Type: The bar chart shows the number of Customers in each Subscription Type, helping to identify which Subscription Types are most popular and contribute the most to the customer base.

      
## Insights:

### Total Active Customers:

  - Tracking the Total Number of Active customers over time helps identify trends in customer acquisition and retention. For example, you might observe that customer growth spiked during a particular period or region.

### Customer Attrition Rate:

  - A key metric for understanding customer loyalty. A high attrition rate could highlight areas where retention efforts need to be improved. You could analyze whether certain subscription types or regions show a higher rate of attrition.

    
### Top 10 Customers:

  - This table helps focus attention on the most valuable Customers in terms of Revenue or other performance metrics. By identifying the top 10 customers and their Subscription Type and Region, you can tailor marketing or retention strategies to maximize value from these key accounts.

    
### Subscription Type Popularity:

  - The bar chart helps visualize which Subscription Types have the highest number of customers. This is useful for understanding customer preferences and can guide decisions on which subscription types to focus on for promotions or improvements. BASIC Subscription has the highest number of customers (10).


![CustomerSegmentDashbord](https://github.com/user-attachments/assets/27e5ac43-346a-4316-a036-6bd4c42b762f)

 

## Subscription Trends Dashboard:

