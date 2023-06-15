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



Question 2: 
SQL Queries:


Question 3:

SQL Queries:


Answer: 


Question 4: 
SQL Queries:

Answer: 



Question 5: 

SQL Queries:

Answer:
