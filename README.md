Beginner SQL Project to learn basic analysis.

Will be analyizing Retail Sales from a company to find top sales
___________________________________________________________________________________________________

-- SQL Retail Sales analysis - P1

-- SQL Retail Sales analysis - P1

-- Create table
```sql
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
```

-- Inserted into table

-- Check if values are inserted
```sql
Select * from retail_sales limit 10;
```

-- Getting count of rows
```sql
Select count(*) from retail_sales;
```

--Checking for nulls
```sql
select * from retail_sales where 
	transactions_id is null
	or
	sale_date is null
	or
	sale_time is null
	or
	gender is null
	or 
	category is null
	or
	quantiy is null
	or 
	cogs is null
	or 
	total_sale is null;
```
-- deleteing null values/ data cleaning
```sql
delete from retail_sales
	where 
	transactions_id is null
	or
	sale_date is null
	or
	sale_time is null
	or
	gender is null
	or 
	category is null
	or
	quantiy is null
	or 
	cogs is null
	or 
	total_sale is null;
```
-- Exploring data

-- how many sales do we have?
```sql
select count(*) as total_sales from retail_sales;
```
-- how many unique customers do we have (Use distinct to get unique customers)
```sql
select count(distinct(customer_id)) as total_sales from retail_sales;
```
-- how many unique categories do we have 
```sql
select count(distinct(category)) as total_category from retail_sales;
```
-- what are the categories
```sql
select distinct category from retail_sales;
```
-- data analysis and business key problems and answers 

--1.Write a SQL query to retrieve all columns for sales made on '2022-11-05:
```sql
select * from retail_sales where sale_date = '2022-11-05';
```
--2. Write a SQL query to retrieve all transactions 

--where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022:
```sql
SELECT 
  *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantiy >= 4
```
-- 3. Write a SQL query to calculate the total sales (total_sale) for each category.
```sql
select category, 
	   sum(total_sale),
	   count(*) as orders from retail_sales group by category;
```
--4. Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:
```sql
select  ROUND(AVG(age), 2), count(*) as orders from retail_sales where category = 'Beauty';
```
--5. Write a SQL query to find all transactions where the total_sale is greater than 1000.
```sql
select * from retail_sales where total_sale >= 1000
```
--6.Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
```sql
select count(*),gender, category from retail_sales group by gender, category;
```
-- 7. Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
```sql
select * from(
	select 
		extract(year from sale_date) as year,
		extract(month from sale_date) as month,
	 	avg(total_sale) as total_sales,
		 RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) order by avg(total_sale) desc) as rank
		from retail_sales
		group by 1,2)
	as t1
	where rank = 1;
```sql
--8 Write a SQL query to find the top 5 customers based on the highest total sales **:
```sql
select 
	distinct(customer_id), 
	sum(total_sale) as total 
	from retail_sales 
	group by customer_id 
	order by 2 desc limit 5;
```
--9 Write a SQL query to find the number of unique customers who purchased items from each category.:
```sql
select 
	count(distinct(customer_id)),
	category
	from retail_sales
group by category;
```	

--10 Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):
```sql
with hourly_sales as(
select *,
	CASE
		when extract(hour from sale_time) <= 12  then 'morning'
			
		when extract(hour from sale_time) between 12 and  17 then 'afternoon'
		
		else 'evening'
		
	end as shift
from retail_sales
)select shift,count(*) AS total_orders from hourly_sales

group by shift
```
-- end of project

