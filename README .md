# Retail Sales

## Project Overview

**Project Title**: Retail Sales  
**Level**: Beginner  
**Database**: `p1_retail_sales_db`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.

## Project Goals

1. **Database Creation**: Build a relational database to store and manage retail sales records.
2. **Data Cleaning**: Identify and remove inconsistencies or missing values in the data.
3. **Exploratory Data Analysis (EDA)**: Understand the structure, trends, and key statistics in the dataset.
4. **Business Querying**: Use SQL to extract insights that answer real business questions.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `p1_retail_sales_db`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.
- **Importing data**: 'retail_sales'.csv file is imported.

```sql
CREATE DATABASE p1_retail_sales_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset. 
- **Deleting null values**:if any null values are found deleting the null record.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1.**What is the total revenue generated from all sales**:
```sql
SELECT SUM(total_sale) AS total_revenue
FROM retail_sales;
```
2.**How many transactions took place in total?**
```sql
SELECT COUNT(*) AS total_transactions
FROM retail_sales;
```

3.**What is the average sale amount per transaction?**
```sql
SELECT AVG(total_sale) AS avg_sale_per_transaction
FROM retail_sales;
```

4.**What is the total sales amount for each product category?**
```sql
SELECT category, SUM(total_sale) AS total_category_sales
FROM retail_sales
GROUP BY category
ORDER BY total_category_sales DESC;
```

5.**Which product category had the highest quantity sold?**
```sql
SELECT category, SUM(quantity) AS total_quantity_sold
FROM retail_sales
GROUP BY category
ORDER BY total_quantity_sold DESC
LIMIT 1;
```

6. **How do total sales differ between male and female customers?**
```sql
SELECT gender, 
COUNT(*) AS number_of_transactions,
SUM(total_sale) AS total_sales,
AVG(total_sale) AS avg_sale_per_transaction
FROM retail_sales
GROUP BY gender;
```


 7. **What is the age group distribution of customers?**
```sql
SELECT 
    CASE 
        WHEN age BETWEEN 18 AND 25 THEN '18-25'
        WHEN age BETWEEN 26 AND 35 THEN '26-35'
        WHEN age BETWEEN 36 AND 45 THEN '36-45'
        WHEN age BETWEEN 46 AND 60 THEN '46-60'
        ELSE '60+'
    END AS age_group,
    COUNT(*) AS number_of_customers
FROM retail_sales
GROUP BY age_group
ORDER BY age_group;
```

8. **What are the total sales for each sale date?**
```sql
SELECT sale_date, SUM(total_sale) AS daily_sales
FROM retail_sales
GROUP BY sale_date
ORDER BY sale_date;
```

9. **Who are the top 5 customers based on total amount spent?**
```sql
SELECT customer_id, SUM(total_sale) AS customer_spending
FROM retail_sales
GROUP BY customer_id
ORDER BY customer_spending DESC
LIMIT 5;
```

10. **What is the profit (total_sale - COGS) for each transaction?**
```sql
SELECT 
    transactions_id,
    total_sale,
    cogs,
    (total_sale - cogs) AS profit
FROM retail_sales
ORDER BY profit DESC
LIMIT 10;
```




## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing , Beauty and Electronics.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
 - **High Revenue Contributors**: Specific queries identify top customers by total sales, providing clarity on which customers contribute most to revenue.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.
- **Sales Trends & Peaks**: Monthly and daily sales trends are explored, including identifying best-selling days, months, or shifts, which can be used for planning promotions and inventory.


## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project provides a solid foundation in SQL for data analysts, encompassing key areas such as database creation, data cleaning, exploratory analysis, and business-oriented querying. The analysis delivers valuable insights into sales performance, customer behavior, product trends, and seasonal patterns—enabling data-driven decision-making across various aspects of the business.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the SQL scripts provided in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries provided in the `sql_p1_query` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author 

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles


Thank you for your !
