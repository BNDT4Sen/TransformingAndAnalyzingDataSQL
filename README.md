# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals

The aim of this project is to clean the data provided in the Ecommerce table to the point where useful information could be gleaned. How realistic this goal is depends largely on how much
valid data is left over to be properly analyzed. Some columns with just a few non-NULL entries cannot be readily relied upon for identifying patterns.

## Process

1.
I first imported the data for the tables, starting with all_sessions.
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
