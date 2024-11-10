## Division of customers for a subscription service

### Project Overview
This project aims to provide insights into the segments and trends of customers who subscribed for a service. By analyzing the various aspects of the available data, I’ll be identifying the different subscription types, and customer behavior. Key trends in subscription cancellations and renewals would also be analyzed; these would serve as the bedrock of recommendations to be made.   

### Data Sources
Customer data, the primary dataset for this analysis was provided by LITA, and it contains detailed information about each subscription made by the customers.

### Tools Used
- Excel – Data cleaning, analysis and visualization [Download here](https://microsoft.com)
- SQL Server – Data Analysis [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- PowerBI – Creating reports [Download here](https://www.microsoft./power-bi/downloads)
-	GitHub - Portfolio building [Log in here](https://github.com/)

### Data Cleaning/Preparation
In the initial data preparation phase, I performed the following tasks:
1.	Data loading and inspection,
2.	Removing duplicates,
3.	Handling missing values,
4.	Data cleaning and formatting

### Exploratory Data Analysis (EDA)
This involved exploring the customer data to answer key questions such as:
1. Calculate the average subscription duration
2. Identify the most popular subscription types
Queries were also written and executed to extract key insights on the following:
-	retrieve the total number of customers from each region. 
-	find the most popular subscription type by the number of customers.
-	find customers who canceled their subscription within 6 months. 
-	calculate the average subscription duration for all customers. 
-	find customers with subscriptions longer than 12 months. 
-	calculate total revenue by subscription type. 
-	find the top 3 regions by subscription cancellations. 
-	find the total number of active and canceled subscriptions.

### Data Analysis
```SQL
select * from [dbo].[NCustomerdata] 

Delete from [dbo].[NCustomerdata] where CustomerID is Null and Region is Null and SubscriptionType is Null 

------------TOTAL NUMBER OF CUSTOMERS FROM EACH REGION------------

Select Region, COUNT (DISTINCT CUSTOMERID) As CustomersByRegion
from [dbo].[NCustomerdata] Group by Region

-------------- Most Popular Subscription Type by the Number of Customers-------------

Select Top (1) SubscriptionType, Count (CustomerID) As CustomerSubscriptionType
from [dbo].[NCustomerdata] Group by SubscriptionType
Order by CustomerSubscriptionType DESC  

---------------CUSTOMERS WHO CANCELED THEIR SUBSCRIPTION WITHIN 6 MONTHS---------

Select * from [dbo].[NCustomerdata] 
where DATEDIFF (month, SubscriptionStart, SubscriptionEnd) <=6
And SubscriptionEnd IS NOT NULL
And Canceled = 1;

--------------AVERAGE SUBSCRIPTION DURATION FOR ALL CUSTOMERS------------------
SELECT AVG(DATEDIFF(MONTH, SubscriptionStart,
COALESCE(SubscriptionEnd, SubscriptionStart))) AS AVG_Duration
from [dbo].[NCustomerdata] 

----------CUSTOMERS WITH SUBSCRIPTION LONGER THAN 12 MONTHS---------------

Select CustomerName,
SubscriptionStart, SubscriptionEnd,
DATEDIFF(MONTH, SubscriptionStart, COALESCE(SubscriptionEnd, SubscriptionStart))
As Duration from [dbo].[NCustomerdata] 
where DATEDIFF (MONTH, SubscriptionStart, COALESCE (SubscriptionEnd, SubscriptionStart))<=12
Order by Duration DESC

------------TOTAL REVENUE BY SUBSCRIPTION TYPE----------

  Select * from [dbo].[NCustomerdata]

Select Region,
Sum (Revenue) As Total_Regional_Revenue
from [dbo].[NCustomerdata]
Group by Region
Order by Total_Regional_Revenue ASC

-----------TOP 3 Regions by Subscription Cancellations--------------

Select Top 3 Region,
Count (SubscriptionEnd) As TotalCancelation 
from [dbo].[NCustomerdata]
where SubscriptionEnd Is Not Null
Group by Region Order by TotalCancelation DESC

-----------Total Number of Active and Canceled Subscriptions-------------

Select CustomerID, count(Canceled) from [dbo].[NCustomerdata] 
where Canceled = 'True'
Group by CustomerID

Select CustomerID, count(Canceled) from [dbo].[NCustomerdata] 
where Canceled = 'False'
Group by CustomerID
```

### Results 

[Adeniyi Olufunso Comprehensive Customer Data.xlsx](https://github.com/user-attachments/files/17690059/Adeniyi.Olufunso.Comprehensive.Customer.Data.xlsx)


![SQL Customer data result 1](https://github.com/user-attachments/assets/6fc7ca6f-240c-47ea-8629-9142c7e8930c)


![SQL Customer data result 2](https://github.com/user-attachments/assets/ef5f3561-7a5b-468d-8655-e18ef2d50475)


![SQL customer data result 3](https://github.com/user-attachments/assets/4af15ea3-5a60-4eb4-86c0-e4951a5da9e0)


![SQL Top 3 Regions --- Customer data](https://github.com/user-attachments/assets/48e714e6-752e-4796-8a2c-94fc440ec167)


