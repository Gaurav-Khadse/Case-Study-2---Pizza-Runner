# Case-Study-2-Pizza-Runner🍕

![image](https://github.com/user-attachments/assets/750d5bcd-7cc3-4918-b758-d8080a5a68ab)

## Contents
- [**Introduction**](#introduction)
- [**Entity Relationship Diagram**](#entity-relationship-diagram)
- [**Data Cleaning & Data Transformation**](#data-cleaning--data-transformation)
- [**Case Study Questions & Solutions**](#case-study-questions--solutions)
  - [**A. Pizza Metrics**](#a-pizza-metrics)
  - [**B. Runner And Customer Experience**](#b-runner-and-customer-experience)
  - [**C. Ingredient Optimisation**](#c-ingredient-optimisation)
- [**Key Insights**](#key-insights)

## Introduction

Welcome to the Pizza Runner Case Study! Follow Danny's journey as he combines the irresistible allure of "80s Retro Styling and Pizza Is The Future" to launch Pizza Runner, an innovative venture in the pizza delivery industry. With his background in data science, Danny understands the significance of data collection for business growth. Now, he seeks assistance in cleaning and analyzing the data to optimize Pizza Runner's operations and guide his runners more efficiently. Join us as we explore how data-driven decisions propel Pizza Runner towards success and elevate the pizza delivery experience to new heights.

## Entity Relationship Diagram

![Screenshot 2025-05-02 202315](https://github.com/user-attachments/assets/f1a0ac00-3dbc-421e-90e6-ae291f29bfbc)


## Data Cleaning & Data Transformation
- customer_orders table Before
  
  ![Customer orders before](https://github.com/user-attachments/assets/2015b128-edac-480f-b2f2-aad8be0a9262)

  - The customer_orders table consists of individual pizza orders, with each row representing a unique pizza.
  - Key columns in the table are pizza_id, exclusions, and extras.
  - Before utilizing the data for queries, the exclusions and extras columns require a data cleaning process to ensure accuracy and consistency.
  - Data cleaning involves handling missing or null values in the exclusions and extras columns.
  - The ingredient_id values in the exclusions and extras columns need to be standardized for uniformity.
  - Inconsistencies and duplicates in the exclusions and extras data should be resolved to eliminate ambiguities.
  - By performing thorough data cleaning, the customer_orders table will be optimized for effective analysis.
  - The cleaned data will provide valuable insights into customer preferences, enabling better decision-making for Pizza Runner's operations.
  - With accurate data, Pizza Runner can efficiently meet customer demands and deliver an enhanced pizza ordering experience.

```sql
 DROP TABLE IF EXISTS customer_orders_temp;

CREATE TABLE customer_orders_temp AS
SELECT 
  order_id,
  customer_id,
  pizza_id,
  CASE 
    WHEN exclusions IS NULL OR exclusions = 'null' THEN ''
    ELSE exclusions
  END AS exclusions,
  CASE 
    WHEN extras IS NULL OR extras = 'null' THEN ''
    ELSE extras
  END AS extras,
  order_time
FROM customer_orders;

```

- customer_orders table After as customer_orders_temp
  
  ![Customer orders After](https://github.com/user-attachments/assets/bd0a1ab0-c0b3-49df-8dbd-226baf2da64c)

- runner_orders table Before

  ![runner_orders table Before](https://github.com/user-attachments/assets/44021ba4-c272-4c70-a68e-c8054a8eeb34)

  The data in the orders table of Pizza Runner contains valuable information regarding the assignment of orders to runners, including pickup times, distances, and durations. However, it is crucial to note that the 
  table may have some known data issues that require careful handling during data cleaning.

   Here are the key points to consider when cleaning the data in the orders table:

  - Verify Data Types: Before proceeding with data cleaning, it is essential to check the data types for each column in the schema SQL. Ensuring accurate data types will prevent potential data type mismatches and 
    errors in subsequent queries.
  - Handle Incomplete Orders: Some orders may not be fully completed and can be canceled by either the restaurant or the customer. It is necessary to identify and properly handle these incomplete orders during the 
    data cleaning process.
  - Address Null Values: The table may contain null values in certain columns, such as pickup_time, distance, and duration. Properly handling these null values is crucial to avoid inaccuracies in the analysis.
  - Validate Timestamps: The pickup_time column represents the timestamp when the runner arrives at Pizza Runner headquarters to pick up the pizzas. Validating and ensuring the consistency of these timestamps will 
    be essential to maintain data integrity.
  - Clean Distance and Duration: The distance and duration fields provide information about the runner's travel to deliver the order. Cleaning these fields involves checking for any outliers or inconsistencies 
    that may affect analysis results.
  - Address Known Data Issues: As there are known data issues in the table, special attention must be given to resolving these issues during the data cleaning process. Identifying and rectifying data discrepancies 
    will enhance the accuracy and reliability of the dataset.
 ```sql
    DROP TABLE IF EXISTS runner_orders_temp;

    CREATE TABLE runner_orders_temp AS
SELECT 
  order_id,
  runner_id,
  CASE 
    WHEN pickup_time IS NULL OR pickup_time = 'null' THEN NULL
    ELSE pickup_time
  END AS pickup_time,
  CASE 
    WHEN distance IS NULL OR distance = 'null' THEN NULL
    WHEN distance LIKE '%km' THEN TRIM(TRAILING 'km' FROM distance)
    ELSE distance
  END AS distance,
  CASE 
    WHEN duration IS NULL OR duration = 'null' THEN NULL
    WHEN duration LIKE '%minutes' THEN TRIM(TRAILING 'minutes' FROM duration)
    WHEN duration LIKE '%minute' THEN TRIM(TRAILING 'minute' FROM duration)
    WHEN duration LIKE '%mins' THEN TRIM(TRAILING 'mins' FROM duration)
    ELSE duration
  END AS duration,
  CASE 
    WHEN cancellation IS NULL OR cancellation = 'null' THEN ''
    ELSE cancellation
  END AS cancellation
FROM runner_orders;

 #Step 2: Alter column types to proper formats in MySQL

ALTER TABLE runner_orders_temp
MODIFY pickup_time DATETIME,
MODIFY distance DECIMAL(5,2),
MODIFY duration INT;
```

- runner_orders table After AS runner_orders_temp
     
![runner_orders_temp](https://github.com/user-attachments/assets/1e85edf0-eef3-4021-9dae-e41a499fd9ce)


## Case Study Questions & Solutions

- A. Pizza Metrics🍕🍕

1.How many pizzas were ordered?
 ```sql
select count(*) as cnt from customer_orders_temp;
```
 Answer:
 
  ![1 Pizza Matrices](https://github.com/user-attachments/assets/a48e0448-f9f8-4a22-80d9-e1903fc69dc0)

  - The SQL query selects the number of pizza orders (pizza_orders) from the customer_orders_temp table.
  - The COUNT(*) function calculates the total number of order IDs in the customer_orders_temp table, effectively giving the count of pizza orders.
  - As a result, the query presents the total count of pizza orders as pizza_orders.
