# E-Commerce-Analytics

# Bank Analytics 

![](bankimage.jpg)


## Table of Contents
---
- [ Project Overview]( #project-overview)
- [Data Sources](#data-sources)
- [ Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [KPI](#kpi)
- [Data Analysis](#data-analysis)
- [Findings](#findings)


### Project Overview
---

Led a project focused on leveraging data analytics to optimize e-commerce operations and enhance customer experience.Utilized MySQL, Power BI and Excel to analyze data and derive actionable insights. Implemented data driven strategies to drive business growth and improve operational efficiency.


### Data Sources
---

In this analysis two data sets were used which contained detailed information about the bank.
- "Finance_1.csv"
- "Finance_2.csv"
### Tools
---
- Excel - Data Cleaning
- MySQL - Data Analysis
- Power BI - Creating Reports


### Data Cleaning
---

In the initial data preparation phase , we performed the following tasks:
1. Data loading and inspection
2. Handling missing values
3. Data cleaning and formatting

### KPI
---
1. Weekday vs Weekend (Order_purchase_timestamp) Payment Statistics
2. Number of Orders with a review score of 5 and payment type as a credit card
3. The average number of days taken for order_delivered_date for pet_shop
4. Average price and payment values from customers of Sau Paulo City
5. Relationship between shipping days (order_delivered_customer_date- order_purchase_timestamp) vs review scores




### Data Analysis
---

```
SELECT * FROM e_commerce_analytics.olist_customers_dataset;
# KPI 1 : Weekday vs Weekend (Order_purchase_timestamp) Payment Statistics

SELECT 
    CASE
        WHEN DAYOFWEEK(STR_TO_DATE(o.order_purchase_timestamp, '%Y-%m-%d')) IN (1 , 7) THEN 'Weekend'
        ELSE 'Weekday'
    END AS DayType,
    COUNT(DISTINCT o.order_id) AS TotalOrders,
    ROUND(SUM(p.payment_value)) AS TotalPayments,
    ROUND(AVG(p.payment_value)) AS AveragePayment
FROM
    orders_dataset o
        JOIN
    payments_dataset p ON o.order_id = p.order_id
GROUP BY DataType;


# KPI 2 : Number of Orders with a review score of 5 and payment type as a credit card

SELECT 
    COUNT(DISTINCT p.Order_id) AS NumberOfOrders
FROM
    payments_dataset p
        JOIN
    reviews_dataset r ON p.order_id = r.order_id
WHERE
    r.Review_score = 5
        AND p.payment_type = 'Credit Card';
        
        
# KPI 3 : The average number of days taken for order_delivered_date for pet_shop

SELECT 
    product_category_name,
    ROUND(AVG(DATEDIFF(order_delivered_customer_date,
                    order_purchase_timestamp))) AS Avg_delivery_time
FROM
    orders_dataset o
        JOIN
    items_dataset i ON i.order_id = o.order_id
        JOIN
    products_dataset p ON p.product_id = i.product_id
WHERE
    p.product_category_name = 'Pet Shop'
        AND o.order_delivered_customer_date IS NOT NULL;
        

# KPI 4 : Average price and payment values from customers of Sau Paulo City
SELECT 
    ROUND(AVG(i.price)) AS Average_Price,
    ROUND(AVG(p.payment_value)) AS Average_Payment
FROM
    customers_dataset c
        JOIN
    order_dataset o ON c.customer_id = o.customer_id
        JOIN
    items_dataset i ON o.order_id = i.order_id
        JOIN
    payments_dataset ON o.order_id = p.order_id
WHERE
    c.city = 'Sau Paulo';
    
    
# KPI 5 : Relationship between shipping days (order_delivered_customer_date- order_purchase_timestamp) vs review scores

SELECT 
    ROUND(AVG(DATEDIFF(order_delivered_customer_date,
                    order_purchase_timestamp)),
            0) AS AvgShippingDays,
    Review_score
FROM
    order_dataset o
        JOIN
    review_dataset r ON o.order_id = r.order_id
WHERE
    order_delivered_customer_date IS NOT NULL
        AND order_purchase_timestamp IS NOT NULL
GROUP BY review_score;
```

```
POWER BI

```
![]






### Findings
---
The analysis results are summarized as follows:
- Loan amount was highest in the year 2013(104 Mn) followed by 2014(99Mn),2012(97Mn),2011(51Mn),2015(35Mn),2016(33Mn),2009(6Mn) and 2008(1Mn)
- Out of Total accounts 68.19% are Verified (326.19 Mn) and 31.81% are Non-Verified(154.55 Mn)
- Out of the total revol_bal, Grade B has the highest(131Mn) followed by Grade A(115 Mn), Grade C(110 Mn), Grade D(75 Mn),Grade E(19 Mn) and Grade F(7 Mn)
- Out of 39717 records for home_ownership ,39,646 are registered. Out of this record , maximum people live on Rental basis(18847) followed by Mortgage(17645), Own(3053),    Other(95) and None(3)
- Out of Total $446 Mn Loan Amount , 358 Mn is fully paid, 68 Mn is charged off and the current status is 19 Mn.
- Top 5 purposes for loan were debt_consolidation(2366 Mn) followed by home_improvement(343.35 Mn),other(322.14 Mn),small_business(248.01 Mn) and major_purchase(178.36 Mn)
- Top 5 state wise total_customers were CA(7099) followed BY NY(3812),FL(2866),TX(2727) and NJ(1850).
  



  



