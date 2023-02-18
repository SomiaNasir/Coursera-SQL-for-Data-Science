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
SELECT COUNT(*) FROM [table_name];  
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
SELECT COUNT(DISTINCT [ID]) FROM [table_name];  
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


