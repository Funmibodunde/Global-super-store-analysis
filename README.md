# Global Superstore Data Analysis
Sales Analysis overtime of Global super store across the globe

## Table of Contents

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools](#tools)

[Data Cleaning](#data-cleaning)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Results](#results)

[Recommendations](#recommendations)

### Project Overview

This data analysis project aim to provide meaningful insight into the Global superstore dataset which would aid management in making informed decision to improve profitability and performance by analyzing various aspect of the sales and profit data, we seek to identify trends, make data driven recommendation and gain deeper understanding on the company performance.

![Github global super store](https://github.com/user-attachments/assets/a2b6ab0a-171d-491e-83dd-90ebb5e0d6d3)


### Data Sources

The primary dataset used for this analysis is the “Global superstore dataset” containing detailed information about each sale made by the company.

### Tools

- Excel - Data Cleaning
- SQL Server - Data Analysis
- Power Bi - Visualization/Creating Reports

### Data Cleaning

In the initial data preparation phase, we performed the following tasks
1.	Data loading
2.	Handling missing values
3.	Data cleaning and formatting 

### Exploratory Data Analysis 

EDA Involved exploring the global superstore data to answer key questions such as;
- What are the three countries that generated the highest total profit for Global Superstore in 2014? b) For each of these three countries, find the three products with the highest 
total profit. Specifically, what are the products’ names and the total profit for each product? 
- Identify the 3 subcategories with the highest average shipping cost in the United States. 
- Assess Nigeria’s profitability (i.e., total profit) for 2014. How does it compare to other African countries? b) What factors might be responsible for Nigeria’s poor performance? You might want to investigate shipping costs and the average discount as potential root causes.
- Identify the product subcategory that is the least profitable in Southeast Asia. Note: For this question, assume that Southeast Asia comprises Cambodia, Indonesia, Malaysia, Myanmar (Burma), the Philippines, Singapore, Thailand, and Vietnam. b) Is there a specific country i n Southeast Asia where Global Superstore should stop offering the subcategory identified in 4a? 
- Which city is the least profitable (in terms of average profit) in the United States? For this analysis, discard the cities with less than 10 Orders. b) Why is this city’s average profit so low? 
- Which product subcategory has the highest average profit in Australia?
- Who are the most valuable customers and what do they purchase?

### Data Analysis

```sql
SELECT 
	TOP(3) 
	Country,
	ROUND(SUM(Profit),2) AS Total_profit
FROM 
	Global_orders
WHERE
	Order_date LIKE '%2014%'
GROUP BY
	Country
ORDER BY
	Total_Profit desc;
```
```sql
SELECT
	TOP 3
	Product_name,
	ROUND(SUM(Profit),2) AS Total_profit2
FROM
	Global_orders
WHERE
	Country = 'United States'
Group by
	Product_name
order by
	Total_profit2 desc;
```
```sql
SELECT
	country,
	SUM(Profit) AS Total_profit
FROM
	Global_orders
WHERE
	region = 'africa'
group by country
order by total_profit asc;
```
```sql
SELECT
	TOP 3
	sub_category,
	ROUND(AVG(shipping_cost),2) AS shipping
FROM
	Global_orders
WHERE
	Country = 'united states'
Group by
	sub_category
order by
	shipping desc;
```
```sql
SELECT
	country,
	ROUND(SUM(shipping_cost),2) AS Total_shipping_cost,
	SUM(DISCOUNT) as discounted
FROM
	Global_orders
WHERE
	region = 'africa'
group by country
order by total_shipping_cost DESC, discounted desc;
```
```sql
SELECT
	Product_name,
	round(sum(shipping_cost),2) as shipping,
	ROUND(SUM(Profit),2) AS Total_profit2,
	sum(discount) as discounted
FROM
	Global_orders
WHERE
	Country = 'nigeria'
Group by
	Product_name
order by
	Total_profit2 desc, discounted desc, shipping desc;
```
```sql
SELECT
	city,
	count (city),
	ROUND(avg(Profit),2) AS avg_least_profit
FROM
	Global_orders
WHERE
	Country = 'united states'
Group by
	city
having
	count(city) > 10
order by
	avg_least_profit asc
```
```sql
SELECT
	sub_category,
	round(sum(shipping_cost),2) as shipping,
	ROUND(avg(Profit),2) AS avg_profit2,
	sum(discount) as discounted
FROM
	Global_orders
WHERE
	City = 'lancaster'
Group by
	sub_category
order by
	avg_profit2 asc, discounted asc, shipping asc;
```

### Results

This analysis results are summarized as follows
1.	United states, India and China are the top 3 that generate highest profit in 2014.
2.	Top product that made the highest profit in united states (canon image advance copier, binding machine and laser jet copier), India (sharp wireless fax digital, hp copy machine and Samsung smart phone) and China (sauder classic bookcase, apple smart phone and cisco smart phone)
3.	Copiers, Machines and Tables has the highest average shipping cost in the United state.
4.	Nigeria made the least profit in 2014, the total loss Nigeria incurred was more than the highest profit made that year. This loss was due to high shipping ad discount cost.
5.	Table is the least profitable subcategory in southeast Asia. Indonesia is one of top countries that orders tables with least profit.
6.	Lancaster city made the least average profit united state due to low average sales.
7.	Top customers are Tom Ashbrooke, Tamara Chand and Greg Tran. They purchased furniture, technology appliance and office supplies.

### Recommendations

Based on the analysis, we recommend the following actions:
- Global super store should not operate in Nigeria or they should try and reduce the shipping and discount cost.
- They should not supply tables to Indonesia.
- Lancaster city should work on increasing their sales through marketing and promoting of products.









