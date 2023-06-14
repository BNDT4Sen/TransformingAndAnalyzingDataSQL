What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

For the all_sessions table:



For the analytics table:
SELECT * FROM analytics
WHERE date IS NULL 
OR fullvisitorid IS NULL 
OR channelgrouping IS NULL 
OR socialengagementtype IS NULL 
OR units_sold IS NULL 
OR units_sold < 0
OR pageview IS NULL 
OR pageview < 0
OR timeonsite IS NULL 
OR timeonsite < 0
OR bounces IS NULL 
OR bounces < 0
OR revenue IS NULL 
OR revenue < 0
OR unit_price IS NULL
OR unit_price < 0

For the products table:
SELECT * FROM products
WHERE sku IS NULL
OR orderedquantity IS NULL 
OR orderedquantity < 0
OR stocklevel IS NULL 
OR stocklevel < 0
OR restockingleadtime IS NULL 
OR restockingleadtime < 0
OR sentimentscore IS NULL 
OR sentimentmagnitude IS NULL

For the sales_by_sku table:
SELECT * FROM sales_by_sku 
WHERE SKU IS NULL OR total_ordered IS NULL OR total_ordered < 0

For the sales_report:
SELECT * FROM sales_report 
WHERE total_ordered < 0 
OR stocklevel < 0 
OR restockeleadtime < 0 
OR sentimentscore IS NULL 
OR sentimentmagnitude IS NULL
OR ratio IS NULL
OR sku IS NULL 
OR total_ordered IS NULL 
OR name IS NULL 
OR stocklevel IS NULL 
OR restockeleadtime IS NULL
