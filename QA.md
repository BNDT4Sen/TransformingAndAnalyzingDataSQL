What are your risk areas? Identify and describe them:

The sample size is very small for some of the columns that were used in queries to answer the questions. In a table of over 15,000 rows, only having 53 occurences of a productquantity > 0 does not inspire confidence for potential analysis via aggregation.
I may have misinterpreted the differences in the columns between the all_sessions and analytics tables, as well as what some individual columns represent. This could mean that my answers to the questions are not all that accurate. For instance, the productquantity and units_sold columns seem as if they should be closely related, but there does not appear to be much correlation.
Some of the data that I cleaned might have contained useful information. I'm not worried about columns made up only of NULL values, but others such as the currencycode column are not as clear. There was only 1 type of non-NULL value in this column (USD), and because this did not seem to be information useful for the analysis I dropped the column altogether.

QA Process:

For every table I searched for both NULLs as well as values outside of the expected range.

For the all_sessions table:

SELECT * FROM all_sessions
WHERE revisedvisitid IS NULL 
OR revisedvisitid < 0
OR fullvisitorid IS NULL
OR fullvisitorid < 0
OR channelgrouping IS NULL
OR time IS NULL
OR time IS < 0
OR country IS NULL
OR city IS NULL
OR totaltransactionrevenue IS NULL
OR totaltransactionrevenue < 0
OR transactions IS NULL
OR transactions < 0
OR timeonsite IS NULL
OR timeonsite < 0
OR pageviews IS NULL
OR pageviews < 0
OR sessionqualitydim IS NULL
OR date IS NULL
OR visitid IS NULL
OR visitid < 0
OR type IS NULL
OR productrefundamount IS NULL
OR productrefundamount < 0
OR productquantity IS NULL
OR productquantity IS < 0
OR productprice IS NULL
OR productprice IS < 0
OR productrevenue IS NULL
OR productrevenue IS < 0 
OR productsku IS NULL
OR v2productname IS NULL
OR v2productcategory IS NULL
OR productvariant IS NULL
OR currencycode IS NULL
OR itemquantity IS NULL
OR itemquantity < 0
OR itemrevenue IS NULL
OR itemrevenue < 0
OR transactionrevenue IS NULL
OR transactionrevenue < 0
OR transactionid IS NULL
OR pagetitle IS NULL
OR searchkeyword IS NULL
OR pagepathlevel1 IS NULL
OR ecommerceaction_type IS NULL
OR ecommerceaction_type < 0
OR ecommerceaction_step IS NULL
OR ecommerceaction_step < 0
OR ecommerceaction_option IS NULL
OR ecommerceaction_option < 0


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
