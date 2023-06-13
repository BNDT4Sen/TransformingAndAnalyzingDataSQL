Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT a.country, a.city, SUM(a.totaltransactionrevenue) AS totalsales
FROM all_sessions AS a
WHERE a.city != 'Unavailable'
GROUP BY a.country, a.city
ORDER BY totalsales DESC

Answer:

Of the 10 cities with the most transaction revenues, 9 are American. The only non-American city is at fifth place: Tel Aviv, Israel.
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

SELECT country, city, productname, sales
FROM (
  SELECT a1.country country,
		 a1.city city,
		 a1.v2productname productname,
		 MAX(a1.country),
         SUM(an.units_sold) sales,
         ROW_NUMBER() OVER (PARTITION BY MAX(a1.city) ORDER BY SUM(an.units_sold) DESC) rn
  FROM all_sessions a1 INNER JOIN analytics AS an
  ON a1.visitid = an.visitid
  GROUP BY a1.country, a1.city, a1.v2productname
) t
WHERE rn = 1 AND sales > 0 AND city != 'Unavailable'
ORDER BY sales DESC;

Answer:

The top selling product in Mountain View was the Grip Highlighter Pen 3 Pack, with 50 units sold. Next in terms of quantity was 44 SPF-15 Slim & Slender Lip Balm ordered for Sunnyvale.
Chicago is tied in third place with San Francisco with 8 units ordered of their most popular products. Despite not having a single product selling over 8 units in San Francisco, it is
still the city with the plurality of transaction revenue.



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT a.country, a.city, SUM(a.totaltransactionrevenue) AS totalsales, 
SUM(a.totaltransactionrevenue)*100 / (
	 SELECT SUM(a1.totaltransactionrevenue) 
	 FROM all_sessions AS a1 
	 WHERE a1.totaltransactionrevenue > 0 AND city != 'Unavailable'
) AS percentoftotal
FROM all_sessions AS a
WHERE a.city != 'Unavailable' AND a.totaltransactionrevenue > 0
GROUP BY a.country, a.city
ORDER BY totalsales DESC

Answer:

Revenue from San Francisco makes up 19.1% of the total. Sunnyvale and Atlanta follow behind at just over 10% each, and the remaining cities make up less than 10% each. Zurich, Switzerland has the smallest share, at just 0.2%.





