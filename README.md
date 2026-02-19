# Ecommerce Sales Analysis using SQL

## Project Overview

**Project Title**: Ecommerce Sales Analysis  
**Level**: Beginner to Intermediate  
**Database**: `ecommerce_db`

This project demonstrates the design and analysis of an E-Commerce database using SQL. It involves creating a relational database schema, inserting sample data, and performing data analysis through real-world business queries. The project focuses on analyzing customer behavior, product performance, sales trends, and revenue insights.

![E-Commerce Sales Analysis](https://raw.githubusercontent.com/aniketghantewad04/Ecommerce-Sales-Analysis-SQL/main/ecommerce_cover.jpg)

## Objectives

- Design and implement an E-Commerce relational database using SQL.
- Populate tables with sample data representing real-world transactions.
- Perform data analysis to answer business-driven questions.
- Identify top customers, products, and revenue-generating categories.
- Extract insights to support data-driven decision-making.

## Project Structure
![E-Commerce Sales Analysis](https://github.com/aniketghantewad04/Ecommerce-Sales-Analysis-SQL/blob/main/Structure.png)

## Database Creation & Schema Design

**Database Creation**  :
Created an E-commerce database named `ecommerce_db` to simulate real-world online retail operations.
```sql
-- Create the database
CREATE DATABASE ecommerce_db;

-- Use the database
USE ecommerce_db;
```
**Table Design**  :
Designed and implemented normalized relational tables for:
- Categories  
- Products  
- Customers  
- Orders  
- Order_Items  
- Shipping_Details  

**Relationships & Constraints**  :
Established foreign key relationships to maintain data integrity between products, categories, customers, and orders.

**Data Population**  :
Inserted realistic sample data across all tables to represent actual e-commerce transactions and customer behavior.

## Table Creation :
```sql
-- Create the categories table
CREATE TABLE Categories (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(255)
);

-- Create the products table
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255),
    description TEXT,
    price DECIMAL(10, 2),
    stock_quantity INT,
    category_id INT,
    FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);

-- Create the customers table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(20),
    address VARCHAR(255)
);

-- Create the orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    status ENUM('pending', 'processing', 'shipped', 'delivered') DEFAULT 'pending',
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

-- Create the order_items table
CREATE TABLE Order_Items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

-- Create the shipping_details table
CREATE TABLE Shipping_Details (
    shipping_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    address VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    zipcode VARCHAR(20),
    country VARCHAR(100),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id)
);

```

## Data Analysis & Findings

**Q.1 Write a SQL query to find the total number of orders placed by each customer ?**

```sql
SELECT o.customer_id,concat(first_name,' ',last_name) as full_name,COUNT(order_id) AS total_orders
FROM orders as o
join customers as c
on o.customer_id=c.customer_id
GROUP BY customer_id;
```
**Q.2. Write a SQL query to retrieve all orders placed in 2024 ?**

```sql
select *
from orders
where year(order_date)=2024;
```
