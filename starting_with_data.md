Question 1: 

SQL Queries:
```sql
SELECT  a.city,
	   SUM(ac.revenue) AS transactionrevenues
FROM all_sessions_cleaned a
JOIN analytics_cleaned ac ON a.fullvisitorid = ac.fullvisitorid
JOIN products p ON a.productsku = p.productsku
WHERE city != country
AND p.productsku IN (SELECT productsku FROM all_sessions_cleaned)
GROUP BY a.city
ORDER BY transactionrevenues DESC
```
Answer: 



Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
