# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals

The aim of this project is to clean the data provided in the Ecommerce table to the point where useful information could be gleaned. How realistic this goal is depends largely on how much
valid data is left over to be properly analyzed. Some columns with just a few non-NULL entries cannot be readily relied upon for identifying patterns.

## Process

1.
I first imported the data for the tables with the following queries:
CREATE TABLE all_sessions (
 	revisedvisitid SERIAL,
 	fullVisitorId NUMERIC,
 	channelGrouping VARCHAR(255),
 	time NUMERIC,  
 	country VARCHAR(255),  
 	city VARCHAR(255),  
 	totalTransactionRevenue NUMERIC,
 	transactions INT,
 	timeOnSite INT,
 	pageviews INT,
 	sessionQualityDim INT,
 	date DATE,
 	visitId INT,
 	type VARCHAR (255),
 	productRefundAmount VARCHAR (255),
 	productQuantity INT,
 	productPrice NUMERIC,
 	productRevenue NUMERIC,
 	productSKU VARCHAR (255),
 	v2ProductName VARCHAR (255),
 	v2ProductCategory VARCHAR (255),
	productVariant VARCHAR (255),
	currencyCode VARCHAR (255),
 	itemQuantity INT,
	itemRevenue NUMERIC,
 	transactionRevenue NUMERIC,
 	transactionId VARCHAR (255),
 	pageTitle VARCHAR (1000),
 	searchKeyword VARCHAR (255),
 	pagePathLevel1 VARCHAR (255),
 	eCommerceAction_type INT,
 	eCommerceAction_step INT,
 	eCommerceAction_option VARCHAR (255),
     PRIMARY KEY (revisedvisitid)
 );
COPY all_sessions
FROM 'Z:/all_sessions.csv'
DELIMITER ','
CSV HEADER;

CREATE TABLE analytics (
	viewid SERIAL,
 	visitNumber INT,
	visitID INT, 
 	visitStartTime INT,
	date date,
 	fullvisitorID NUMERIC,
 	userid INT,
	channelGrouping VARCHAR,
	socialEngagementType VARCHAR,
 	units_sold INT,
	pageview INT,
  timeonsite INT,
 	bounces INT,
 	revenue NUMERIC,
 	unit_price NUMERIC,
    PRIMARY KEY (viewid)
);
COPY analytics
FROM 'Z:/analytics.csv'
DELIMITER ','
CSV HEADER;

CREATE TABLE products (
 SKU VARCHAR,
 name VARCHAR,
 orderedQuantity INT, 
 stockLevel INT,
 restockingLeadTime INT,
 sentimentScore NUMERIC,
 sentimentMagnitude NUMERIC,
 PRIMARY KEY (SKU)
);
COPY products
FROM 'Z:/products.csv'
DELIMITER ','
CSV HEADER;

CREATE TABLE sales_by_sku (
SKU VARCHAR,
total_ordered INT,
PRIMARY KEY (SKU)
);
COPY sales_by_sku 
FROM 'Z:/sales_by_sku.csv'
DELIMITER ','
CSV HEADER;

CREATE TABLE sales_report (
  SKU VARCHAR,
 	total_ordered INT,
 	name VARCHAR,
 	stockLevel INT,
 	restockeLeadTime INT,
 	sentimentScore NUMERIC,
 	sentimentMagnitude NUMERIC,
 	ratio NUMERIC,
 PRIMARY KEY (SKU)
);
COPY sales_report
FROM 'Z:/sales_report.csv'
DELIMITER ','
CSV HEADER;

2.
Next I entered some general queries just to take a look at how the data is structured in the tables, and how each column relates to the others.
3.
I began my QA process by checking each column for both NULL values and values that exist outside of the possible range. For example, columns that were denominated in dollars,
could not have values below 0. The queries I used can be found in QA.md
4.
After identifying some of the issues with the data I began cleaning. A mostly comprehensive list of the queries I used can be found in cleaning_data.md
5.
Once the glaring issues within the data were taken care of, I started on creating queries to answer the initial 5 questions. Those queries can be found in starting_with_questions.md
6.
I then took another look at the data in order to think of some interesting questions that the Ecommerce database could answer. These questions and their related queries are in the starting_with_data.md

## Results

(fill in what you discovered this data could tell you and how you used the data to answer those questions)
From my understanding, the all_sessions table refers to user interactions with one website in particular, whereas analytics covers a larger pool of users and their interactions. The analytics table is dramatically larger in terms of rows, and many of the visitids in analytics do not match with those in all_sessions. Of the 1,000,000 rows in analytics, only around 40,000 of them can be related back to the all_sessions table.

## Challenges 

I faced a ton of challenges while going through this project. My biggest mistake was when I accidentally deleted the all_sessions.visitid column. This was after I had already completed my QA and data cleaning,
and so I decided to find a way to reinsert this data back into the table. After around ~4 hours of scouring forums and trying a bunch of different methods, I ended up just starting from scratch. That ended up taking a lot less time. 
Another challenge that I faced was reconciling the visitid/fullvisitorid columns in the all_sessions and analytics tables. Trying to figure out the difference between analytics.units_sold and all_sessions.productquantity became another long winded investigation. 

## Future Goals

I would try to gain a stronger understanding of how the different tables relate to one another, and ideally figure out the context in which they exist. As it currently stands, I feel unsure about some of the answers I arrived to. If I had more information about the tables I feel like I could write stronger queries.  
