# SQL for Data Science
Course: [SQL for Data Science (Coursera)](https://www.coursera.org/learn/sql-for-data-science)

## Peer-graded Assignment: Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset
This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate your intent as required.

### Yelp Dataset ER Diagram
The entity relationship (ER) diagram below, should help familiarize you with the design of the Yelp Dataset provided for this peer review activity.

![](https://github.com/SomiaNasir/Coursera-SQL-for-Data-Science/blob/main/YelpERDiagram.png?raw=true)

## Part 1: Yelp Dataset Profiling and Understanding

### 1. Profile the data by finding the total number of records for each of the tables below:
~~~sql  
SELECT COUNT(*) 
FROM table_name;  
~~~  
i. Attribute table = 10000  
ii. Business table = 10000  
iii. Category table = 10000  
iv. Checkin table = 10000  
v. elite_years table = 10000  
vi. friend table = 10000  
vii. hours table = 10000  
viii. photo table = 10000  
ix. review table = 10000  
x. tip table = 10000  
xi. user table = 10000  

### 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.  
~~~sql  
SELECT COUNT(DISTINCT ID) 
FROM table_name;  
~~~
i. Business = 10000 (id)  
ii. Hours = 1562 (business_id)  
iii. Category = 2643 (business_id)  
iv. Attribute = 1115 (business_id)  
v. Review = 10000 (id)  
vi. Checkin = 493 (business_id)  
vii. Photo = 10000 (id)  
viii. Tip = 537 (user_id), 3979 (business_id)  
ix. User = 10000 (id)  
x. Friend = 11 (user_id)  
xi. Elite_years = 2780 (user_id)  

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	

### 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."
Answer: no  
SQL code used to arrive at answer:
~~~sql
SELECT * 
FROM user 
WHERE id IS NULL OR 
  name IS NULL OR  
  review_count IS NULL OR 
  yelping_since IS NULL OR  
  useful IS NULL OR  
  funny IS NULL OR 
  cool IS NULL OR 
  fans IS NULL OR 
  average_stars IS NULL OR 
  compliment_hot IS NULL OR 
  compliment_more IS NULL OR 
  compliment_profile IS NULL OR 
  compliment_cute IS NULL OR 
  compliment_list IS NULL OR 
  compliment_note IS NULL OR 
  compliment_plain IS NULL OR 
  compliment_cool IS NULL OR
  compliment_funny IS NULL OR 
  compliment_writer IS NULL OR
  compliment_photos IS NULL;
~~~  

### 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:  
~~~sql
SELECT MIN(column_name), MAX(column_name), AVG(column_name)
FROM table_name;  
~~~
i. Table: Review, Column: Stars  
	
		min: 1		max: 5		avg: 3.7082  
		
ii. Table: Business, Column: Stars  
	
		min: 1.0	max: 5.0	avg: 3.6549  
		
iii. Table: Tip, Column: Likes  
	
		min: 0		max: 2		avg: 0.0144  
		
iv. Table: Checkin, Column: Count  
	
		min: 1		max: 53		avg: 1.9414  
		
v. Table: User, Column: Review_count  
	
		min: 0		max: 2000	avg: 24.2995  
    
### 5. List the cities with the most reviews in descending order:  
SQL code used to arrive at answer:
~~~sql
SELECT city, SUM(review_count) AS total_reviews
FROM business
GROUP BY city
ORDER BY total_reviews DESC;
~~~
Copy and Paste the Result Below:

| city            | total_reviews |
|-----------------|---------------|
| Las Vegas       |         82854 |
| Phoenix         |         34503 |
| Toronto         |         24113 |
| Scottsdale      |         20614 |
| Charlotte       |         12523 |
| Henderson       |         10871 |
| Tempe           |         10504 |
| Pittsburgh      |          9798 |
| Montréal        |          9448 |
| Chandler        |          8112 |
| Mesa            |          6875 |
| Gilbert         |          6380 |
| Cleveland       |          5593 |
| Madison         |          5265 |
| Glendale        |          4406 |
| Mississauga     |          3814 |
| Edinburgh       |          2792 |
| Peoria          |          2624 |
| North Las Vegas |          2438 |
| Markham         |          2352 |
| Champaign       |          2029 |
| Stuttgart       |          1849 |
| Surprise        |          1520 |
| Lakewood        |          1465 |
| Goodyear        |          1155 |  

(Output limit exceeded, 25 of 362 total rows shown)  
### 6. Find the distribution of star ratings to the business in the following cities:
#### i. Avon    

SQL code used to arrive at answer:
~~~sql
SELECT stars, SUM(review_count) AS total_reviews
FROM business
WHERE city = 'Avon'
GROUP BY stars;
~~~
Copy and Paste the Resulting Table Below (2 columns – star rating and count):

| stars | total_reviews |
|-------|---------------|
|   1.5 |            10 |
|   2.5 |             6 |
|   3.5 |            88 |
|   4.0 |            21 |
|   4.5 |            31 |
|   5.0 |             3 |

#### ii. Beachwood    

SQL code used to arrive at answer:
~~~sql
SELECT stars, SUM(review_count) AS total_reviews
FROM business
WHERE city = 'Beachwood'
GROUP BY stars;
~~~
Copy and Paste the Resulting Table Below (2 columns – star rating and count):
| stars | total_reviews |
|-------|---------------|
|   2.0 |             8 |
|   2.5 |             3 |
|   3.0 |            11 |
|   3.5 |             6 |
|   4.0 |            69 |
|   4.5 |            17 |
|   5.0 |            23 |  

### 7. Find the top 3 users based on their total number of reviews:
		
SQL code used to arrive at answer:
~~~sql
SELECT name, review_count
FROM user
ORDER BY review_count DESC
LIMIT 3;
~~~
Copy and Paste the Result Below:

| name   | review_count |
|--------|--------------|
| Gerald |         2000 |
| Sara   |         1629 |
| Yuri   |         1339 |  

### 8. Does posing more reviews correlate with more fans?
Please explain your findings and interpretation of the results:  
SQL CODE:  
~~~sql
SELECT name, review_count, fans
FROM user
ORDER BY review_count DESC;
~~~
RESULT:

| name      | review_count | fans |
|-----------|--------------|------|
| Gerald    |         2000 |  253 |
| Sara      |         1629 |   50 |
| Yuri      |         1339 |   76 |
| .Hon      |         1246 |  101 |
| William   |         1215 |  126 |
| Harald    |         1153 |  311 |
| eric      |         1116 |   16 |
| Roanna    |         1039 |  104 |
| Mimi      |          968 |  497 |
| Christine |          930 |  173 |
| Ed        |          904 |   38 |
| Nicole    |          864 |   43 |
| Fran      |          862 |  124 |
| Mark      |          861 |  115 |
| Christina |          842 |   85 |
| Dominic   |          836 |   37 |
| Lissa     |          834 |  120 |
| Lisa      |          813 |  159 |
| Alison    |          775 |   61 |
| Sui       |          754 |   78 |
| Tim       |          702 |   35 |
| L         |          696 |   10 |
| Angela    |          694 |  101 |
| Crissy    |          676 |   25 |
| Lyn       |          675 |   45 |  

(Output limit exceeded, 25 of 10000 total rows shown)

INTERPRETATION:  
The above table shows the number of reviews sorted in the descending order and no particular pattern is seen in the fans column so it can be concluded that there is no correlation between the two columns. However, it can further investigated by finding correlation coefficient between the number of reviews and fans.  
### 9. Are there more reviews with the word "love" or with the word "hate" in them?
Answer:  
| love | hate |
|------|------|
| 1780 |  232 | 
	
SQL code used to arrive at answer:
~~~sql
SELECT 
(SELECT COUNT(id)
FROM review
WHERE text LIKE '%love%') AS love, 
(SELECT COUNT(id)
FROM review
WHERE text LIKE '%hate%') AS hate;
~~~
### 10. Find the top 10 users with the most fans:

SQL code used to arrive at answer:
~~~sql
SELECT name, fans
FROM user
ORDER BY fans DESC
LIMIT 10;
~~~
Copy and Paste the Result Below:

| name      | fans |
|-----------|------|
| Amy       |  503 |
| Mimi      |  497 |
| Harald    |  311 |
| Gerald    |  253 |
| Christine |  173 |
| Lisa      |  159 |
| Cat       |  133 |
| William   |  126 |
| Fran      |  124 |
| Lissa     |  120 |
## Part 2: Inferences and Analysis

### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.  

I have choosen city = Las Vegas and category = Restaurants.  

#### i. Do the two groups you chose to analyze have a different distribution of hours?  

SQL CODE:
~~~sql
SELECT stars, COUNT(DISTINCT id) AS number_of_restuarants, 
    COUNT(hours) AS number_of_opening_days, 
    COUNT(hours)/COUNT(DISTINCT id) AS avg_opening_days,
    SUM(review_count) AS total_reviews
FROM business b JOIN hours h
ON b.id = h.business_id
JOIN Category c
ON c.business_id = b.id
WHERE city = 'Las Vegas' AND category = 'Restaurants'
GROUP BY stars;
~~~
RESULTS:

| stars | number_of_restuarants | number_of_opening_days | avg_opening_days | total_reviews |
|-------|-----------------------|------------------------|------------------|---------------|
|   3.0 |                     1 |                      7 |                7 |           861 |
|   4.0 |                     2 |                     14 |                7 |          6552 |  

Both groups do not have any differences in their distribution of hours.  

#### ii. Do the two groups you chose to analyze have a different number of reviews?  
Yes, both have different number of reviews.  

#### iii. Are you able to infer anything from the location data provided between these two groups? Explain.  

SQL code used for analysis:
~~~sql
SELECT stars, neighborhood, address, postal_code
FROM business b JOIN Category c
ON c.business_id = b.id
WHERE city = 'Las Vegas' AND category = 'Restaurants'
ORDER BY stars;
~~~

| stars | neighborhood | address                         | postal_code |
|-------|--------------|---------------------------------|-------------|
|   3.0 |              | 5045 W Tropicana Ave            | 89103       |
|   4.0 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
|   4.0 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
|   4.5 | Eastside     | 3480 S Maryland Pkwy            | 89169       |  

There is no relation between location and star rating of the restaurants.  
### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
#### i. Difference 1: 
There are more open businesses than closed ones.  
#### ii. Difference 2: 
There are more number of reviews for opened businesses than closed ones.  

SQL code used for analysis:
~~~sql
SELECT is_open, COUNT(DISTINCT id) AS total_businesses, 
    AVG(stars) AS avg_stars, SUM(review_count) AS total_reviews
FROM business 
GROUP BY is_open;
~~~
| is_open | total_businesses |     avg_stars | total_reviews |
|---------|------------------|---------------|---------------|
|       0 |             1520 | 3.52039473684 |         35261 |
|       1 |             8480 | 3.67900943396 |        269300 |  

### 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:  
	
#### i. Indicate the type of analysis you chose to do:  

Which city has the best services in the category of hotels and travels?  
         
#### ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:  

I have calculated the total number of businesses, total number of operating businesses, average star rating and total number of review counts for category of
hotels and travel for all cities available in the dataset.  
From the following table, we can see that Oakwood Village had 1 hotel with a poor rating and it was closed later. The best performing hotel is in Scottsdale with 
a rating of 4.5 which is followed by Las Vegas.  
#### iii. Output of your finished dataset:

| city                | No_of_business | avg_stars | total_reviews | No_of_open_business |
|---------------------|----------------|-----------|---------------|---------------------|
| Scottsdale          |              1 |       4.5 |           223 |                   1 |
| Las Vegas           |              2 |       4.0 |            51 |                   2 |
| Mantua              |              1 |       4.0 |             8 |                   1 |
| Phoenix             |              1 |       3.5 |            80 |                   1 |
| Stuttgart           |              1 |       3.5 |             3 |                   1 |
| Stuttgart-Vaihingen |              1 |       2.0 |             4 |                   1 |
| Pineville           |              1 |       2.0 |             3 |                   1 |
| Oakwood Village     |              1 |       1.5 |             9 |                   0 |
#### iv. Provide the SQL code you used to create your final dataset:
~~~sql
SELECT city, COUNT(DISTINCT id) AS No_of_business, 
    AVG(stars) AS avg_stars, SUM(review_count) AS total_reviews, 
    SUM(is_open) AS No_of_open_business
FROM business JOIN category
ON id = business_id
WHERE category = 'Hotels & Travel' 
GROUP BY city
ORDER BY AVG(stars) DESC, SUM(is_open) DESC, SUM(review_count) DESC;
~~~

         
	
