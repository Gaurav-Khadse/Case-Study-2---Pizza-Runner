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
  - The customer_orders table consists of individual pizza orders, with each row representing a unique pizza.
  - Key columns in the table are pizza_id, exclusions, and extras.
  - Before utilizing the data for queries, the exclusions and extras columns require a data cleaning process to ensure accuracy and consistency.
  - Data cleaning involves handling missing or null values in the exclusions and extras columns.
  - The ingredient_id values in the exclusions and extras columns need to be standardized for uniformity.
  - Inconsistencies and duplicates in the exclusions and extras data should be resolved to eliminate ambiguities.
  - By performing thorough data cleaning, the customer_orders table will be optimized for effective analysis.
  - The cleaned data will provide valuable insights into customer preferences, enabling better decision-making for Pizza Runner's operations.
  - With accurate data, Pizza Runner can efficiently meet customer demands and deliver an enhanced pizza ordering experience.
