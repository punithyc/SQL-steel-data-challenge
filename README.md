# SQL-steel-data-challenge

*__I am a sharing Steel data challange Insights - A Data Analysis Case Study performed on SQL in my journey into Data Science.__*

## Intoduction

The steel data challange contains 5 Tables as Customers, Orders, baskets, products & Country table to solved this case study as a Customer Insights analyst for The General Store.<br>
As a Customer Insights Analyst for 'The General Store' i have to analyze the following data to find out crucial information about the customers & provide to marketing team .

* *__customers__*
* *__country__*
* *__products__*
* *__baskets__*
* *__orders__*

  ## Problem Statements for Challenges
  
* *__1. What are the names of all the countries in the country table?__*
* *__2. What is the total number of customers in the customers table?__*
* *__3. What is the average age of customers who can receive marketing emails (can_email is set to 'yes')?__*
* *__4. How many orders were made by customers aged 30 or older?__*
* *__5. What is the total revenue generated by each product category?__*
* *__6. What is the average price of products in the 'food' category?__*
* *__7. How many orders were made in each sales channel (sales_channel column) in the orders table?__*
* *__8.What is the date of the latest order made by a customer who can receive marketing emails?__*
* *__9. What is the name of the country with the highest number of orders?__*
* *__10. What is the average age of customers who made orders in the 'vitamins' product category?__*

  ## Tools Used
  [Mysql](https://www.hackerrank.com/profile/punithyc8688)

  ## Challenge analysis using sql

* *__1. What are the names of all the countries in the country table?__*
```
select distinct country_name from country
```
* *__2. What is the total number of customers in the customers table?__*
```
select count(customer_id) as total_customers from customers
```
* *__3. What is the average age of customers who can receive marketing emails (can_email is set to 'yes')?__*
```
select avg(age) as avg_age from customers
where can_email like '%yes%'
```
* *__4. How many orders were made by customers aged 30 or older?__*
```
select count(order_id) as total_orders from customers as c
join orders as o on c.customer_id=o.customer_id 
where c.age>=30
 --            (or)
 select count(*) as total_orders from orders
 where customer_id in (select customer_id from customers
                    where age>=30)
```
* *__5. What is the total revenue generated by each product category?__*
```
select p.category,sum(p.price) as total_revenue from products p
join baskets as b on p.product_id=b.product_id
join orders o on b.order_id=o.order_id
group by p.category
```
* *__6. What is the average price of products in the 'food' category?__*
```
select avg(price) as avg_price from products
where category like '%food%'
```
* *__7. How many orders were made in each sales channel (sales_channel column) in the orders table?__*
```
select sales_channel,count(*) as orders_count from orders
group by sales_channel
```
* *__8.What is the date of the latest order made by a customer who can receive marketing emails?__*
```
select max(date_shop) as latest_order from orders as o
join customers as c on c.customer_id=o.order_id
where can_email='yes'
select max(date_shop) as latest_order from orders
where customer_id in (select customer_id from customers
                         where can_email='yes')
```
* *__9. What is the name of the country with the highest number of orders?__*
```
select country_name,count(*) as orders from country as c
join orders as o on o.country_id=c.country_id
group by country_name
order by orders desc
limit 1
```

* *__10. What is the average age of customers who made orders in the 'vitamins' product category?__*
```
select p.category,round(avg(c.age)) as avg_age from customers as c
join orders as o on c.customer_id=o.customer_id
join baskets as b on o.order_id=b.order_id
join products as p on b.product_id=p.product_id
where p.category='vitamins'
group by p.category
```
## Conclusion
The analysis of Steel data challange through SQL has provided valuable insights into various aspects of the business. By querying the database, I've been able to uncover crucial information regarding sales trends, customer preferences, popular items.

*__for more information__* : [Steel data challange](https://www.steeldata.org.uk/sql3.html)

## For any Queries/Doubts
[website](https://bio.link/punithyc)

