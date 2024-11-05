# LITA-Capstone-Project-Customer-Data
---
##  PROJECT TITLE: CUSTOMER'S SUBSCRIPTION DATA
---
##  DATA SOURCE
This data was provided by The Incubator Hub.
##  PROJECT OVERVIEW
This dataset contains Subscriptions data of customers, the project aims to analyse subscription trends and patterns in order to draw key insights that will facilitate better decision making. The dataset contains both qualitative and quantitative data.

---
##  KEY VARIABLE
This segment explains the important variables that were used for the analysis.

**Qualitative Data**
-  **Subscription Type:** this represents the categories of subscriptions that customers can subscribe to. It represents the subscription package.
-  **Region:** this represents the geographical area that customers reside in, in which subscription is made.
- **Subscription Cancelation**: this represents the customers who canceled (True) and did not cancel (False) their subscription.

 **Quantitative Data**
-  **Subscription Start/End**: this represents the start date of subscription till the end date of subscription.
-  **Revenue:** this represents the total value of subscription. it also represents the amount spent by customers for subscription.
-  **Subscription Duration**: this represents the number of days that the subscription lasted for.
---
##  TOOLS USED
For this dataset, i used three(3) analytical tools for it. They are;
-  Microsoft Excel [Download here](https://www.microsoft.com/en-us/microsoft-365/excel)
-  SQL Server [Download here](https://www.microsoft.com/en-us/power-platform/products/power-bi)
-  Microft Power BI [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-download)
---
##  DATA PREPARATIONS
In order to be able to analyse this data i had to make sure it was cleaned. Firstly, i checked for duplicates and removed all duplicates. This reduced thedata by 50%.I also checked for empty cells which there was none. When i was sure it the data is properly cleaned i started my analysis. I also used the cleaned data in SQL and Power BI.
###  Excel Analysis
I used Excel Functions and Pivot Tables to carry out the following operations;
Pivot Tables was used to find Subscription Pattterns. The Subscription patterns i aimed to draw insight from are as follows;
-  Revenue by Subscription Type and Region (to see which Subscription type is dominant in the various regions)
-  Revenue by Subscription Cancellation and Subscription Type (to see which subscription type had the most cancellations)
-  Revenue by Subscription Duration and Subscription Type (to see how long customers subscribed to a package)
-  Average Revenue by Subscription Type
-  Average Revenue by Region

![Project Lita - Excel 03-Nov-24 11_17_32 PM](https://github.com/user-attachments/assets/81fb0a82-f945-4c16-8d1d-27d2bfb16dbb)

I used Excel functions to calculate Subscription Duration by Subtracting Subscription End from Subscription Start. 
I then calculated the average subscrription duration by using the Average function and The most popular subscription type by using the Count function.
I also calculated the Maximum and Minimum Revenue by using the Max and Min function.

![Project Lita - Excel 03-Nov-24 11_18_05 PM](https://github.com/user-attachments/assets/458ce27d-a19c-48bb-b57a-3dcdbee541b4)

---
###  SQL QUERIES
To Further the analysis in the dataset i ran some queries using SQL. The queries are as follows;
- To see the whole data
```
select * from [dbo].[Customer Data]
```
-  To retrieve the total number of customers from each region.
```
select count (customername) as TotalNoCustomersbyRegion, Region
from [dbo].[Customer Data]
group by Region 
```
-  To find the most popular subscription type by the number of customers.
```
select count (customername) as MostPopularSubType, SubscriptionType
from [dbo].[Customer Data]
group by SubscriptionType
Basic is the most popular subscription type
```
-  To find customers who canceled their subscription within 6 months.
```
Select * from [dbo].[Customer Data]
where DATEDIFF(month, SubscriptionStart, SubscriptionEnd) <=6
And SubscriptionEnd is not null
And canceled= 1;
```
- To calculate the average subscription duration for all customers.
```
SELECT AVG(Subscription_Duration_Days) AS AVERAGESUBSCRIPTIONDURATION
FROM [dbo].[Customer Data]
```
-  To find customers with subscriptions longer than 12 months.
``` 
Select * From [dbo].[Customer Data]
Where Subscription_Duration_Days >365
```
-  To calculate total revenue by subscription type.
```
select Sum (Revenue) as TotalRevenuebyProducts, SubscriptionType
from [dbo].[Customer Data]
group by SubscriptionType
```
-  To  find the top 3 regions by subscription cancellations.
```
select top 3 Region,Count (Canceled) As SubscriptionsCancellations
from [dbo].[Customer Data]
Where Canceled=1 
Group by Region
Order by 2 desc
```
-  To find the total number of active and canceled subscriptions.
```
select count (Canceled) as NoActiveandCancelledSub
from [dbo].[Customer Data]
where Canceled=0
or Canceled=1
Group by canceled 
```
---
###  DATA VISUALIZATION WITH POWER BI
In order to present all my analysis in a Dashboard i took my findings to Power BI.

![Project Lita - Excel 03-Nov-24 11_20_29 PM](https://github.com/user-attachments/assets/e534ae5f-e8a9-4e5f-bc76-9ab1ea37d5e4)

####  INSIGHTS DRAWN
1.  The Total Revenue generated in the subscription year is 67,540,175. The Maximum revenue generated for a Subscription is 3,000 and the Minimum revenue generated for a subscription is 1,000. ( Note: the total revenue is inclusive of those who canceled subscription).  The Total Revenue without Subscription Cancellation is 37,208,727.
2.  The Average Subscription duration is 365 days.
3.  The Eastern Region generated the Highest Revenue for customers who subscribed the most with 16,958,763.
4.  The Basic Subscription Type generated the most revenue with a total of 33,776,735 inclusive with those who canceled. Without Customers who cancelled The Basic Subscription type sums up to 23,683,493.
5. The rate of Subscription Cancelation is high in this subscription with a percentage of 45% while for customers who retained subscription is 55%. Even if those retaining subscription is higher than those who canceled, i consider the rate of cancelation high.
6. In the Eastern Region, all the customers retained their subscription, but this is not the case in other regions. The Northern, Western and Southern regions lost 60% of their customers.
7. Most Customers cancelled their Premium and Standard package which resulted in a revenue loss of 10,126,800 and 10,111,406 respectively.



