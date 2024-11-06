# Subscription-Analysis-Dashboard

## Project Overview
---

This project aims to analyze customer data from a subscription service to uncover insights into customer behavior, subscription patterns, and key trends in cancellations and renewals. The final deliverable is an interactive Power BI dashboard that presents these insights.


![Overview](https://github.com/user-attachments/assets/e0f6ac65-81b5-4b86-b548-80adfb7eabc1)


## Data Source

The data used for this project was provided by our tutors as part of the LITA Capstone Project. It includes customer subscription data, which is essential for analyzing subscription trends, customer behavior, and cancellation patterns. The dataset consists of various fields, including customer ID, subscription type, start and end dates, and revenue, among others. The dataset was used to perform the analysis and generate the insights presented in the Power BI dashboards.






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

To visualize trends in subscriptions, cancellations, and renewals over time, and to track the performance of subscription offerings with detailed metrics.

#### Key Visualizations

- Card Visualizations:

   - Total Subscribers: Displays the total number of active subscriptions which is 20.
   - Subscription Length: Shows the average subscription length across customers, which is 0.02 years.
   - Subscription Growth Rate: Represents the subscription growth rate, which is a high value of 15,000%, indicating a substantial increase in subscriptions over the period.

- Slicer Filters:

   - Subscription Type: Allows for the analysis of subscription trends based on different types of subscriptions.
   - Cancellation: Helps filter the data by whether subscriptions were canceled or not.
   - Year/Month: Provides flexibility to analyze trends on a yearly or monthly basis.

- Stacked Column Chart:

   - Annual Subscription & Revenue: Displays the annual subscription and revenue trends over time, This chart accounts for both start and end dates of subscriptions.

- Bar Chart Visualization:

   - Total Subscription by Cancellation Status: This bar chart shows the total number of subscriptions based on their cancellation status. The chart categorizes subscriptions into two groups: True (canceled) and False (not canceled).
The count of subscriptions for the False category is higher than True, indicating more active subscriptions.

- Area Chart Visualization:

   - Total Subscription by Start and End Date: The area chart helps visualize the volume of subscriptions over time based on their start and end dates. This chart helps identify subscription growth and churn over different periods.
     
## Insights

### Total Subscribers

  - The Total Subscribers card visual helps track the overall number of active subscriptions, providing a clear indicator of customer engagement. With 20 subscribers in this case, you can monitor if this number increases or decreases over time.

### Subscription Length:

  - The Subscription Length metric gives insight into how long customers are staying with the service, with a value of 0.02 years indicating a short average subscription length. This may prompt further analysis into customer retention strategies or subscription offerings.

### Subscription Growth Rate:

  - The Subscription Growth Rate of 15,000% indicates an extremely rapid increase in subscriptions. This is a noteworthy metric and may suggest a successful marketing campaign, promotion, or external factors that significantly boosted subscription numbers.

### Annual Subscription & Revenue:

  - The Annual Subscription & Revenue stacked chart provides a breakdown of annual subscription data and revenue. The chart includes both start and end dates, offering a more comprehensive view of how subscriptions are performing over the year, with blue and orange colors differentiating subscription and revenue trends.

### Subscription Cancellations:

  - The Total Subscription by Cancellation bar chart gives a clear view of how many subscriptions were canceled (True) versus still active (False). With more False subscriptions, you can conclude that most customers are staying subscribed, but continued tracking can help improve retention strategies.

### Total Subscription by Start and End Date:

  - The Area Chart allows for a comprehensive view of how subscriptions are distributed across different start and end dates. This helps identify growth or churn during specific periods.



![Subscription Trends](https://github.com/user-attachments/assets/febdf630-5cbc-4dda-affc-638b2512fb02)


## Cancellation Trends Dashboard

The Cancellation Trends Dashboard helps track the trends and distribution of subscription cancellations. It focuses on identifying the causes of cancellations and the revenue impact, providing insights into customer churn.

#### Key Visualizations:

- Slicer Filters:

   - Cancellation: Allows filtering data to show canceled vs. active subscriptions.
   - Revenue: Filters for analyzing trends based on subscription revenue.
   - Subscription Type: Filters data by various subscription types.
   - Start and End Year: Allows tracking the cancellations and revenue impact over different time periods.

- Card Visualizations:

   - Count of Cancellations: Displays the total number of cancellations, with a value of 20 cancellations.
   - Sum of Revenue: Shows the total revenue from cancellations, which is 41k.

- Stacked Column Chart:

   - Cancellation Revenue: A stacked chart that shows the revenue impact of cancellations, with a higher proportion of False (Non-Canceled) subscriptions contributing to more revenue compared to True (Canceled) subscriptions

- Doughnut Pie Chart:

   - Cancellation Distribution: Visualizes the distribution of cancellations, with False (Non-Canceled) subscriptions represented by a lighter blue (4k or 55% of the total) and True (Canceled) subscriptions represented by a darker blue (3k or 45%).

## Insights

### Count of Cancellations:

  - The Count of Cancellations card shows the total number of cancellations (20). This metric is important for understanding the level of churn in the customer base. By tracking cancellations over time, we can spot trends and investigate if any external factors are causing spikes in cancellations.
Sum of Revenue:

  - The Sum of Revenue card shows that the total revenue generated from subscriptions that were canceled amounts to 41k. This metric helps to understand the revenue loss due to cancellations and can be a key indicator of potential customer dissatisfaction or service issues.

### Cancellation Revenue (Stacked Column Chart):

  - The Cancellation Revenue stacked column chart visually represents how much revenue is lost due to cancellations compared to the revenue retained. A higher number of False (Non-Canceled) subscriptions suggests that more customers are staying subscribed, whereas a higher number of True (Canceled) subscriptions would indicate a loss in revenue.

### Cancellation Distribution (Doughnut Pie Chart):

  - The Cancellation Distribution doughnut pie chart shows the percentage of cancellations. False (Non-Canceled) subscriptions account for 55% of the revenue (4k), while True (Canceled) subscriptions account for 45% (3k). This gives a quick overview of how much of the customer base is still active compared to those who have canceled.

![Cancellations](https://github.com/user-attachments/assets/e0a9de5e-8b59-4d2c-8f38-4705934abe93)

## Limitations

1. Missing or Incomplete Data

Some key columns were missing or incomplete in the dataset, such as subscription duration data, customer demographics (age,gender) which could have provided more insights. 


2. Limited Subscription Types:

The analysis was limited by the available subscription types in the dataset. This may not represent the full range of subscription options or trends in the broader market, which could have provided a more comprehensive view of customer behavior.

3. Assumptions Made for Certain Metrics:

Certain metrics, such as subscription length lost due to cancellations, were calculated based on available data and assumptions, which may not fully reflect the true values in all cases. These assumptions could introduce some margin of error into the analysis.

4.Limited Scope of Analysis:

The analysis focused mainly on customer behavior, subscription types, and cancellations. Other factors like customer demographics, marketing efforts, or regional trends were not fully incorporated due to the scope of the dataset and project constraints.

5. Tool Limitations:

Some Power BI features or visualizations were limited by the dataset’s complexity and size. For example, large volumes of data could result in slower performance or limited interactivity within the Power BI dashboard.

6. Time Constraints:

Due to time limitations, some analyses or visualizations that could have provided additional insights were not fully explored. Further analysis could yield more granular insights into customer trends and subscription behavior.

## References

i. Videos:

- Power BI Dashboard Tutorial - YouTube – Video tutorial for building Power BI dashboards and visualizations.
- SQL Server Query Writing - YouTube – YouTube video on SQL query writing and optimization for beginner to intermediate users.

ii. Consultation:

- Personal consultation with a colleague or mentor for insights and feedback on Power BI visualizations and SQL query optimizations.


  📝
  
  🔍
  
  📊
  
  💻
  
  📈
  
  💡


