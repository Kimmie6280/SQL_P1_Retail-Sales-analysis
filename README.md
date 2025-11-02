Beginner SQL Project to learn basic analysis.

Will be analyizing Retail Sales from a company to find top sales
___________________________________________________________________________________________________

Creat Datbase

Create Database SQL_P1
Create Table retail_sales(
				transactions_id INT primary key,
				sale_date DATE,
				sale_time TIME,
				customer_id INT,	
				gender VARCHAR(15),	
				age INT,
				category VARCHAR(15),	
				quantiy Float,
				price_per_unit float,	
				cogs float,	
				total_sale float
);
