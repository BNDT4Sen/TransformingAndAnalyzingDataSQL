What issues will you address by cleaning the data?

Certain columns are made up solely of NULL values, and they will need to be removed completely.
The data types must be appropriate for each column of each table. 
Some tables may not have a column that can act as a natural primary key, and so one might need to be added.


Queries:
Below, provide the SQL queries you used to clean your data.


-- Dropping some unnecessary columns from all_sessions
ALTER TABLE all_sessions
DROP COLUMN productrefundamount,
DROP COLUMN currencycode,
DROP COLUMN itemrevenue,
DROP COLUMN itemquantity,
DROP COLUMN searchkeyword

-- NULL values in a variety of columns were changed to more accurately reflect what they represent.
UPDATE all_sessions
SET timeonsite = '0'
WHERE timeonsite IS NULL

UPDATE all_sessions
SET totaltransactionrevenue = '0'
WHERE totaltransactionrevenue IS NULL;

UPDATE all_sessions
SET transactions = '0'
WHERE transactions IS NULL;

UPDATE all_sessions
SET timeonsite = '0'
WHERE timeonsite IS NULL;

UPDATE all_sessions
SET sessionqualitydim = '0'
WHERE sessionqualitydim IS NULL;

UPDATE all_sessions
SET productquantity = '0'
WHERE productquantity IS NULL;

UPDATE all_sessions
SET productrevenue = '0'
WHERE productrevenue IS NULL;

UPDATE all_sessions
SET transactionrevenue = '0'
WHERE transactionrevenue IS NULL;

UPDATE all_sessions
SET transactionid = 'No Transaction'
WHERE transactionid IS NULL;

UPDATE all_sessions
SET ecommerceaction_option = 'N/a'
WHERE ecommerceaction_option IS NULL;

UPDATE all_sessions
SET v2productcategory = 'Category not Found'
WHERE v2productcategory = '(not set)' OR v2productcategory IS NULL;

UPDATE all_sessions
SET productvariant = 'N/a'
WHERE productvariant = '(not set)' OR productvariant IS NULL;

-- Some of the columns in the all_sessions table had dramatically inflated dollar values. I fixed this with:
ALTER TABLE all_sessions
ALTER COLUMN totaltransactionrevenue TYPE NUMERIC USING (totaltransactionrevenue / 1000000)::NUMERIC,
ALTER COLUMN productprice TYPE NUMERIC USING (productprice / 1000000)::NUMERIC,
ALTER COLUMN productrevenue TYPE NUMERIC USING (productrevenue / 1000000)::NUMERIC,
ALTER COLUMN transactionrevenue TYPE NUMERIC USING (transactionrevenue / 1000000)::NUMERIC

-- The userid table was made up solely of NULLs and was therefore dropped.
ALTER TABLE analytics
DROP COLUMN userid

-- NULL values from the timeonsite column were changed to 0
UPDATE analytics
SET timeonsite = '0'
WHERE timeonsite IS NULL
--The same was done to the units_sold, bounces, pageview, and revenue columns. 

-- The following queries were used to resolve inflated column values and the excess of decimal places:
ALTER TABLE analytics
ALTER COLUMN unit_price TYPE NUMERIC USING (unit_price / 1000000)::NUMERIC,
ALTER COLUMN revenue TYPE NUMERIC USING (revenue / 1000000)::NUMERIC
ALTER TABLE analytics
ALTER COLUMN unit_price TYPE NUMERIC(10,2),
ALTER COLUMN revenue TYPE NUMERIC (10,2)

-- visitstarttime was converted from UNIX EPOCH to time of day using:
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE TIMESTAMP USING TO_TIMESTAMP(visitstarttime::NUMERIC)
ALTER TABLE analytics 
ALTER COLUMN visitstarttime TYPE TIME USING visitstarttime::TIME

-- The sentimentscore and sentimentmagnitude columns in the products table had only one row with NULL values. I chose to leave that as is due to how these two columns scale from negative to positive. 

-- I then identified the ratio column of the sales_report table as referring to the ratio of total_ordered to stocklevel. I renamed this column to be a bit more descriptive and then changed its NULL values to -- 0. The NULL values originally resulted from dividing by 0.
ALTER TABLE sales_report
RENAME ratio TO stock_ratio;

-- There were some other lost queries I used to clean, but they generally just followed the same process as above. 



