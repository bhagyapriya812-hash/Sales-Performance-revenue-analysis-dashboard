use sales_analysis;
INSERT INTO sales
(order_id,customer_name,product,category,quantity,unit_price,region,sales)
VALUES
(1,'Ravi','Laptop','Electronics',2,50000.00,'South',100000.00),
(2,'Priya','Phone','Electronics',3,20000.00,'South',60000.00),
(3,'Anil','Chair','Furniture',5,3000.00,'East',15000.00),
(4,'Sita','Table','Furniture',2,7000.00,'West',14000.00),
(5,'Rahul','Headphones','Electronics',4,2500.00,'North',10000.00);
SELECT* FROM sales;
ALTER TABLE sales
MODIFY category VARCHAR(100);
SELECT* FROM sales;

SELECT* FROM sales;
SELECT customer_name,sales
FROM sales;
SELECT MAX(sales) AS highest_sales
FROM sales;
SELECT MIN(sales) AS lowest_sales
FROM sales;
SELECT SUM(sales) AS total_sales
FROM sales;
SELECT AVG(sales) AS average_sales
FROM sales;
SELECT COUNT(sales) AS count_sales
FROM sales;
SELECT region, sum(sales) AS
total_sales
FROM sales
GROUP BY region;
SELECT customer_name,sales
FROM salesS
ORDER BY sales DESC;
SELECT*
FROM sales
WHERE region = 'south';
SELECT region,sum(sales) AS total_sales
FROM sales
GROUP BY region
HAVING SUM(sales) > 20000;
SELECT DISTINCT region
FROM sales;
SELECT*
FROM sales
WHERE customer_name LIKE 'R%';
SELECT*
FROM sales
WHERE region IN ('south','east');
SELECT*
FROM sales
WHERE sales BETWEEN 15000 AND 100000;
SELECT customer_name,sales,
CASE 
     WHEN sales >= 50000 THEN 'High Sales'
     WHEN sales >= 20000 THEN 'Medium Sales'
     ELSE 'Low Sales'
END AS sales_level
FROM sales;     
SELECT customer_name,sales,region,
COALESCE(region,'unknown') AS region_name
FROM sales;
CREATE TABLE customer(
    customer_id INT,
    customer_name VARCHAR(100),
    city VARCHAR(100)
);
INSERT INTO customer VALUES
(1,'Ravi','Nellore'),
(2,'Priya','Hyderabad'),
(3,'Anil','Chennai'),
(4,'Sita','Bangalore'),
(5,'Rahul','Vijayawada');
SELECT* FROM customer;
SELECT
customer.customer_id,
customer.customer_name,
customer.city,
sales.product,
sales.sales
FROM customer
INNER JOIN sales
ON customer.customer_id =sales.order_id;
SELECT
customer.customer_id,
customer.customer_name,
customer.city,
sales.product,
sales.sales
FROM customer
LEFT JOIN sales
ON customer.customer_id =sales.order_id;
SELECT
customer.customer_id,
customer.customer_name,
customer.city,
sales.product,
sales.sales
FROM customer
RIGHT JOIN sales
ON customer.customer_id =sales.order_id;
SELECT
customer.customer_id,
customer.customer_name,
customer.city,
sales.product,
sales.sales
FROM customer
INNER JOIN sales
ON customer.customer_id =sales.order_id
WHERE sales.sales > 50000;
SELECT
customer.customer_name,
SUM(sales.sales) AS total_sales
FROM customer
INNER JOIN sales
ON customer.customer_id =sales.order_id
GROUP BY customer.customer_name;
SELECT MAX(sales) AS highest_sales
FROM sales;
SELECT MIN(sales) AS lowest_sales
FROM sales;
SELECT AVG(sales) AS average_sales
FROM sales;
SELECT product,SUM(quantity) AS total_quantity
FROM sales
GROUP BY product
ORDER BY total_quantity DESC;
SELECT category,SUM(sales) AS total_sales
FROM sales
GROUP BY caterory;
SELECT product,SUM(sales) AS total_sales
FROM sales
GROUP BY product
ORDER BY total_sales DESC;
SELECT region,COUNT(*) AS total_orders
FROM sales
GROUP BY region
ORDER BY total_orders DESC;
CREATE VIEW sales_dashboard AS SELECT
order_id,customer_name,product,category,quantity,unit_price,region,sales
FROM sales;
SELECT* FROM sales_dashboard;
