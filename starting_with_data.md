Question 1: 
How many products in the all_sessions table had variants?

SQL Queries:

SELECT productsku FROM all_sessions
WHERE productvariant != 'N/a' AND productvariant != 'Single Option Only'
GROUP BY productsku

Answer: 
16 distinct products had variants that were selected.


Question 2: 
What is the earliest and latest user interaction with the website?

SQL Queries:

SELECT MIN(date), MAX(date) 
FROM all_sessions

Answer:
The starting date for the all_sessions table was 2016-08-01, and the most recent was 2017-08-01. 



Question 3: 
Which product had the largest single transaction?

SQL Queries:

SELECT an.units_sold, an.revenue, a.visitid, a.v2productname
FROM analytics AS an
JOIN all_sessions AS a ON a.visitid = an.visitid
WHERE revenue > 0 AND units_sold > 0 
ORDER BY revenue DESC

Answer:
Visitid 1495994469 had the single largest transaction with the purchase of 5 Nest Learning Thermostats for $396.00.


Question 4: 
What products have an ordered quantity greater than the stock level in the products table?

SQL Queries:

SELECT * 
FROM products 
WHERE orderedquantity > stocklevel
ORDER BY orderedquantity DESC

Answer:
15 different products have a greater amount ordered than in stock. Kick Ball is the product with the largest discrepancy, with 15,170 ordered and just 723 in stock.


Question 5: 

SQL Queries:

Answer:
