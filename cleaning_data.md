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




