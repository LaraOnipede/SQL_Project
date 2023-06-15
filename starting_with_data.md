Question 1: which cities and countries have the highest level of transaction revenues on the site?

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
Top 5 cities with highest revenue: Mountain View, Sunnyvale, New York, San Francisco, San Jose
Top 5 countries with highest revenue: United States, India, Japan, United Kingdom, canada


Question 2: What is the average number of products ordered from visitors in each city and country

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
--Average number of product ordered in each city is 16752
--Average number of product ordered in each country is 47380


Question 3: Is there any pattern in the type(product categories) of products ordered from visitors in each city and country

SQL Queries:
```sql
--to reveal pattern in types of product ordered for each city
SELECT city, MAX(v2productcategory) AS most_popular_category, COUNT(*) AS category_count
FROM all_sessions_cleaned
WHERE city != country
GROUP BY city
ORDER BY city;
--to reveal pattern in types of product ordered for each country
SELECT country, MAX(v2productcategory) AS most_popular_category, COUNT(*) AS category_count
FROM all_sessions_cleaned
WHERE city != country
GROUP BY country
ORDER BY country;
```

Answer: Yes, there is a pattern. majority of the orders were made from home, through youtube for most of the cities and countries



Question 4: what is the top-selling product from eachcity/country? can we find any pattern worthy of noting in the products sold?

SQL Queries:
```sql
--to get the top selling products from each city
SELECT city, v2productname, total_sold
FROM (
    SELECT a.city,
           a.v2productname,
           SUM(ac.units_sold) AS total_sold,
           ROW_NUMBER() OVER (PARTITION BY a.city ORDER BY SUM(ac.units_sold) DESC) AS rn
    FROM all_sessions_cleaned a
    JOIN analytics_cleaned ac ON a.visitid = ac.visitid
    WHERE a.city != a.country
    GROUP BY a.city, a.v2productname
) AS product_subquery
WHERE rn = 1
ORDER BY total_sold DESC
--to get the top selling product from each country
SELECT country, v2productname, total_sold
FROM (
    SELECT a.country,
           a.v2productname,
           SUM(ac.units_sold) AS total_sold,
           ROW_NUMBER() OVER (PARTITION BY a.country ORDER BY SUM(ac.units_sold) DESC) AS rn
    FROM all_sessions_cleaned a
    JOIN analytics_cleaned ac ON a.visitid = ac.visitid
    WHERE a.city != a.country
    GROUP BY a.country, a.v2productname
) AS subquery
WHERE rn = 1
ORDER BY total_sold DESC

```
Answer: the provided by the queries above reveals the top-selling product for each city/country



Question 5: 

SQL Queries:

Answer:
