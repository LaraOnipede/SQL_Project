Question 1: Write a query to show the channel with the greatest and lowest lead to the websitelead 

SQL Queries:
```sql
SELECT channelgrouping, COUNT(*) AS count_channelgrp
FROM all_sessions
WHERE channelgrouping != '(Other)'
GROUP BY channelgrouping
ORDER BY count_channelgrp ASC
```
Answer: 
### Organic search is the channel with the greatest lead
### Display is the channel with lowest lead

Question 2: What are the top 3 countries with the highest number of visitors to the website?
SQL Queries:
```sql
SELECT country, COUNT(*) AS count_country
FROM all_sessions
GROUP BY country
ORDER BY count_country DESC
```
Answer:United States, India and United kingdom

Question 3:

SQL Queries:


Answer: 


Question 4: 
SQL Queries:

Answer: 



Question 5: 

SQL Queries:

Answer:
