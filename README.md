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
In order to present all my analysis in a Dashboard i took my findings to Power BI where i visualized key customer segments and subscription patterns.

![Project Lita - Excel 03-Nov-24 11_20_29 PM](https://github.com/user-attachments/assets/e534ae5f-e8a9-4e5f-bc76-9ab1ea37d5e4)

####  INSIGHTS DRAWN
1.  The Total Revenue generated in the subscription year is 67,540,175. The Maximum revenue generated for a Subscription is 3,000 and the Minimum revenue generated for a subscription is 1,000. ( Note: the total revenue is inclusive of those who canceled subscription).  The Total Revenue without Subscription Cancellation is 37,208,727.
2.  The Average Subscription duration is 365 days.
3.  The Eastern and Northern Region customers subscribed to the Basic package, the Southern Region customers subscribed to the Premium package and the Western region customers subscribed to the Standard package.
4.  The Eastern Region generated the Highest Revenue for customers who subscribed the most with 16,958,763.
5.  The Basic Subscription Type generated the most revenue with a total of 33,776,735 inclusive with those who canceled. Without Customers who cancelled The Basic Subscription type sums up to 23,683,493.
6. The rate of Subscription Cancelation is high in this subscription with a percentage of 45% while for customers who retained subscription is 55%. Even if those retaining subscription is higher than those who canceled, i consider the rate of cancelation high.
7. In the Eastern Region, all the customers retained their subscription, but this is not the case in other regions. The Northern, Western and Southern regions lost 60% of their customers.
8. Most Customers cancelled their Premium and Standard package which resulted in a revenue loss of 10,126,800 and 10,111,406 respectively.
---
#### DASHBOARDS WITH APPLIED SLICER
I applied a slicer to my Dashboard in order to get more indepth insights. I applied  Subscription Duration and Subscription Type to my slicer.
####  Dashboard with applied Subscription Duration slicer
The dashboard below shows the applied slicer for 365 days subscription duration.

![Project Lita - Excel 03-Nov-24 11_19_40 PM](https://github.com/user-attachments/assets/a30ddca8-a35e-473f-9ec3-5dc9760753b6)
####  Insights Drawn
1.  The total revenue generated in 365 days is 43,889,663 those  who canceled inclusive
2.  The Basic Subscription Type generated the most revenue with 23,683,493 those who canceled inclusive. The revenue generated for those who did not cancel is 16.97 million. For the Premium package all the customers canceled their subscription
3.  In 365 days, No customer from the Eastern region canceled their subscription which generated a revenue of 10,242,555. But it is not the same with the Northern, Southern and Western Regions with 50% and 33% customers canceling subscription Northern and Western region respectively while all the customers canceled the subscription in the Southern Region.
4.  Overall in 365 days, 54% of customers did not cancel while 46% canceled.

  **The dashboard below shows the applied slicer for 366 days subscription duration.**

![Project Lita - Excel 03-Nov-24 11_20_56 PM](https://github.com/user-attachments/assets/8b394f47-3335-4b4c-90dd-c7cab2829666)
####  Insights Drawn
1.  The total revenue generated in 366 days is 23,650,512 those who canceled inclusive.
2.  The Basic Subscription Type generated the most revenue with 10,093,004 those who canceled inclusive. The revenue generated for those who did not cancel is 6.72 million. For the Standard package all the customers canceled their subscription.
3.  No customer canceled their subscription in 366 days in The Eastern and Southern Region. But all the customers in the Western and Northern region canceled their subscription.
4.  Overall in 366 days, 57% of customers did not cancel their subscription while 47% canceled.

####  Dashboard with applied Subscription Type slicer
For the subscription type slicer, I chose to use the Subscription type that generated the most revenue. The dashboard below shows the applied slicer for the Basic Subscription Type.

![Project Lita - Excel 03-Nov-24 11_21_23 PM](https://github.com/user-attachments/assets/b0e8cdf8-add5-4fd8-adb9-62ac02a9abc0)
####  Insights Drawn
1.  The total revenue generated for the Basic subscription type is 33,776,735 those who canceled inclusive.
2.  The Basic subscription type is well dominated in the Eastern Region and Northern region though 60% of customers in the North canceled thier subscription. while no one in the East canceled.
3.  Overall, 70% of customers did not cancel their basic subscription while 30% canceled.
---
##   GENERAL CONCLUSIONS
Having analysed and seen the insights drawn, here are some generalization i took note of.
- In as much as the rate of Customers who did not cancel is higher than those who canceled, the difference is just by 10% which is not a lot. At this rate, it is safe to say that in coming years customers are likely to cancel their subscription packages if nothing is done about it.
**What can be done?**
- The company would have to look into the sales of the past years to know if customers has been canceling gradually, if this is the case, it is most likely because they increased their subscription packages prices which made users unsubscribe.
- They should look into reducing their prices a bit to retain customers, because if nothing is done at that rate, more customers are bound to be lost.
- Also, all the regions should be looked into especially in the Northern, Western and Southern regions where most of the customers unsubscribed. Call these customers to hear their views on why they stopped subscribing, this way the company have carried out a research and the company will know better ways to satisfy the customers.
- Lastly, even if subscription prices will be increased make sure customers get the worth of their money. Make sure each subscription type has something unique that will be almost irresistible for customers to cancel.
