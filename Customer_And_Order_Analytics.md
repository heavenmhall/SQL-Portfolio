##In this SQL, I'm querying a database with multiple tables in it to quantify statistics about customer and order data. 

#1. How many orders were placed in January?
```sql
SELECT * 
FROM BIT_DB.JanSales
WHERE length(orderid) = 6
AND orderid <> 'Order ID';
```


#2. How many of those orders were for an iPhone? 
```sql
SELECT * 
FROM BIT_DB.JanSales
WHERE product = "iPhone" 
AND length(orderid) = 6;
```

#3. Select the customer accouint numbers for all of the orders that were placed in February.
```sql
SELECT distinct acctnum
FROM BIT_DB.customers cust
INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id = Feb.orderid
WHERE length(orderid) = 6
AND orderid <> 'Order ID';
```

#4. Which prodcut was the cheapest one sold in January, and what was the price?
```sql
SELECT product, price
FROM BIT_DB.JanSales
ORDER BY price ASC LIMIT 5;
```

#5. What is the total revenue for each product sold in January?
```sql
SELECT sum(quantity)*price as revenue
, product
FROM BIT_DB.JanSales
GROUP BY product;
```

#6. Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue? 
```sql
SELECT sum(quantity), product,
sum(quantity)*price as revenue 
FROM BIT_DB.FebSales
WHERE location = "548 Lincoln St, Seattle, WA 98101";
GROUP BY product;
```

#7. How many customers ordered more than 2 products at a time in February, and what was the average amount spent for those customers? 
```sql
SELECT count(distinct cust.acctnum),
avg(quantity*price)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid = cust.order_id
WHERE Feb.Quantity > 2
AND length(orderid) = 6
AND orderid <> 'Order ID';
```

#8. Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
```sql
SELECT distinct location, count(orderID)
FROM BIT_DB.JanSales
WHERE location LIKE '%NY%'
AND length(orderid) = 6
AND orderid <> 'Order ID'
GROUP BY location
HAVING count(orderID)>2;
```

#9. How many of each type of headphone were sold in February?
```sql
SELECT sum(Quantity) as quantity, Product
FROM BIT_DB.FebSales
WHERE Product like '%Headphones%'
GROUP BY Product;
```

#10. What was the average amount spent per account in February? 
```sql
SELECT avg(quantity*price)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid = cust.order_id
WHERE length(orderid) = 6
AND orderid <> 'Order ID';
```

#11. What was the average quantity of products purchased per account in February?
```sql
SELECT sum(quantity)/count(cust.acctnum)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid = cust.order_id 
WHERE length(orderid) = 6
AND orderid <> 'Order ID';
```

#12. Which product brought in the most revenue in January and how much revenue did it bring in total?
```sql
SELECT product, sum(quantity*price)
FROM BIT_DB.JanSales
GROUP BY product
ORDER BY sum(quantity*price) DESC
LIMIT 1;
```




































