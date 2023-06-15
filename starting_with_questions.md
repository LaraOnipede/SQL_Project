Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```sql
--to get city with the highest level of transaction revenues
SELECT  a.city,
	   SUM(ac.revenue) AS transactionrevenues
FROM all_sessions_cleaned a
JOIN analytics_cleaned ac ON a.fullvisitorid = ac.fullvisitorid
JOIN products p ON a.productsku = p.productsku
WHERE city != country
AND p.productsku IN (SELECT productsku FROM all_sessions_cleaned)
GROUP BY a.city
ORDER BY transactionrevenues DESC
--to get country with the highest level of transaction revenues
SELECT  a.country,
	   SUM(ac.revenue) AS transactionrevenues
FROM all_sessions_cleaned a
JOIN analytics_cleaned ac ON a.fullvisitorid = ac.fullvisitorid
JOIN products p ON a.productsku = p.productsku
WHERE city != country
AND p.productsku IN (SELECT productsku FROM all_sessions_cleaned)
GROUP BY a.country
ORDER BY transactionrevenues DESC

```



Answer:




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







