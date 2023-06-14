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
What were the 5 visits that generated the most revenue for the website and where were they from?

SQL Queries:

SELECT an.visitid, a.country, a.city, SUM(an.revenue) AS spentduringvisit
FROM analytics AS an
FULL JOIN all_sessions AS a ON a.visitid = an.visitid
WHERE a.visitid = an.visitid
GROUP BY a.country, a.city, an.visitid
ORDER BY spentduringvisit DESC LIMIT 5

Answer:
All of the top 5 visits were from the United States, with the largest being from Sunnyvale at $649.16. Next was from an undefined American town with $396, a Chicago order with $306, San Jose with $153, and San Francisco at $61.98.
