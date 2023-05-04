# Case-Study1-Dannys-Diner
# Danny_Ma_SQL_Challenge_Case_Study_1
I have created a solution for Case Study 1 of Danny Ma's 8-week SQL challenge. The solution utilizes SQL Aggregate functions, JOINS, and Common Table Expressions (cte) for data manipulation.<br><br>
![temp](https://8weeksqlchallenge.com/images/case-study-designs/1.png)

## Introduction
Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen. <br>

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business. <br>

## Problem Statement
Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite. Having this deeper connection with his customers will help him deliver a better and more personalised experience for his loyal customers.
<br>
He plans on using these insights to help him decide whether he should expand the existing customer loyalty program - additionally he needs help to generate some basic datasets so his team can easily inspect the data without needing to use SQL.

Danny has provided you with a sample of his overall customer data due to privacy issues - but he hopes that these examples are enough for you to write fully functioning SQL queries to help him answer his questions!

Danny has shared with you 3 key datasets for this case study:

* sales <br>
* menu <br>
* members <br>
You can inspect the entity relationship diagram below.
## Entity Relationship Diagram

![Screenshot (257)](https://user-images.githubusercontent.com/129122755/236097463-4c66d216-1a9e-4652-9226-bb0f9f6c7c45.png)



## Case Study Questions
---

**1. What is the total amount each customer spent at the restaurant?**
 ```
    SELECT s.customer_id, SUM(m.price) AS total_amount_spent
	FROM [dbo].[sales] s
	JOIN [dbo].[menu] m
		ON s.product_id = m.product_id
	GROUP BY s.customer_id
	ORDER BY 1,2 DESC;

```

| customer_id | total_amt_spent($) |
| ----------- | ------------------ |
| A           | 76                 |
| B           | 74                 |
| C           | 36                 |

---

**2. How many days has each customer visited the restaurant? Generate two queries to produce the output/result.**
---
    -- Query 1
	SELECT customer_id, COUNT(DISTINCT order_date)
	FROM [dbo].[sales]
	GROUP BY customer_id
	ORDER BY 2;
  
     -- Query 2
	WITH cte AS ( 
		SELECT DISTINCT s.customer_id, s.order_date AS days
	FROM [dbo].[sales] s)
	SELECT customer_id, COUNT(days) AS total_days_visited
	FROM cte
	GROUP BY customer_id
	ORDER BY 2 DESC;
 ---

| customer_id | total_days_visited
| ----------- | ---------------- |
| B           | 6                |
| A           | 4                |
| C           | 2                |
---
