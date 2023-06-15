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
**Top 5 cities with highest revenue: Mountain View, Sunnyvale, New York, San Francisco, San Jose**
**Top 5 countries with highest revenue: United States, India, Japan, United Kingdom, canada**

**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
```sql
--for the average number of products sold in each city
WITH CTE_productordered AS (SELECT a.city,
	  SUM(p.orderedquantity) AS total_productordered
	  FROM all_sessions_cleaned a
      JOIN products p ON a.productsku = p.productsku
      WHERE p.productsku IN (SELECT productsku FROM all_sessions_cleaned)
      GROUP BY city
      ORDER BY total_productordered DESC)
SELECT AVG(total_productordered) AS average_product_ordered
FROM CTE_productordered
--for the average number of products sold in each country
WITH CTE_productordered AS (SELECT a.country,
	  SUM(p.orderedquantity) AS total_productordered
	  FROM all_sessions_cleaned a
      JOIN products p ON a.productsku = p.productsku
      WHERE p.productsku IN (SELECT productsku FROM all_sessions_cleaned)
      GROUP BY country
      ORDER BY total_productordered DESC)
SELECT AVG(total_productordered) AS average_product_ordered
FROM CTE_productordered
```
Answer:
**-Average number of product ordered in each city is 16752**
**Average number of product ordered in each country is 47380**

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







