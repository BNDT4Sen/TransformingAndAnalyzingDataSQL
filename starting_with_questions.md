Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT a.country, a.city, SUM(a.totaltransactionrevenue) AS totalsales
FROM all_sessions AS a
WHERE a.city != 'Unavailable'
GROUP BY a.country, a.city
ORDER BY totalsales DESC

Answer:

Of the top 10 cities with the highest transaction revenues, 9 are American. The only non-American city is at fifth place: Tel Aviv, Israel.
The city with the most sales, San Francisco, has a wide lead over the city with the second most sales, Sunnyvale.

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

-- SELECT a.country, a.city, AVG(an.units_sold) AS averagesold, SUM(an.units_sold) AS totalsold
-- FROM analytics AS an
-- JOIN all_sessions AS a ON an.visitid = a.visitid
-- WHERE an.units_sold > 0
-- GROUP BY a.country, a.city
-- ORDER BY averagesold DESC, totalsold DESC

Answer:

Mountain View is the city with the largest average order size. In second place is the aggregation of all unspecified Canadian cities, followed by 4 more American cities with an average order size greater than 1.



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT a.country, a.city, COUNT(a.v2productcategory) AS categorycount, a.v2productcategory AS productcategory
FROM all_sessions AS a
JOIN analytics AS an ON an.visitid = a.visitid
WHERE an.units_sold > 0
AND city != 'Unavailable'
GROUP BY a.country, a.city, a.v2productcategory
ORDER BY country DESC, city, categorycount DESC

Answer:

Sunnyvale has by far the greatest recurrence of orders from a single product category, at 18 for housewares. Mountain View orders have the greatest category diversity.
Apparel-related categories seem to be the most popular, at least in the US. Most other countries do not have their cities specified, and so we can't go into too much further detail with them.
Canada follows the US in terms of category diversity.

**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







