What issues will you address by cleaning the data?
Duplicates
Missing records
missing columns
NULL values
Outliers


Queries:
Below, provide the SQL queries you used to clean your data.
```sql
--Cleaning all_sessions table
--retrieve information about all sessions table
SELECT
	  column_name, data_type
FROM information_schema.columns
WHERE table_name = 'all_sessions' --returns column_name and data-type for all columns in all_sessions

--Explore all_sessions_table column after column
--retrieved all data from all sessions table 
SELECT *
FROM all_sessions --returns 15134 rows
--check for duplicates
SELECT DISTINCT(fullvisitorid)
FROM all_sessions--returns 14223 row, column fullvisitorid contains duplicates
--confirm duplicates
SELECT fullvisitorid, COUNT(*) AS count_fullvisitor_id
FROM all_sessions
GROUP BY fullvisitorid
ORDER BY count_fullvisitor_id DESC
--confirm miss values
SELECT *
FROM all_sessions
WHERE fullvisitorid IS NULL -- no missing values for fullvisitorid column

--access channelgrouping column
SELECT DISTINCT(channelgrouping)
FROM all_sessions --returned 7 rows, with one stated as others.
 
--for further knowledge about the (Other) channel
SELECT *
FROM all_sessions
WHERE channelgrouping = '(Other)' ----Returned 5 rows. 

--what's the distribution like among the channels
SELECT channelgrouping, COUNT(*) AS count_channelgrp
FROM all_sessions
GROUP BY channelgrouping
ORDER BY count_channelgrp ASC
--organic search is the channel with the highest lead to the ecommerce website
--display has the lowest lead to the webiste

--To Access the country column
SELECT DISTINCT country
FROM all_sessions-- 136 distinct countries
--To identify anomalies in the country column
SELECT country, COUNT(*) AS count_country
FROM all_sessions
GROUP BY country
ORDER BY count_country DESC --returns 24 record where country is (not set)
--Check for missing records in the country column
SELECT *
FROM all_sessions
WHERE country IS NULL --there are no NULL values in the column country

--use Sql CASE statement to impute data for instances where country is (not set)

--To access the city column
SELECT DISTINCT city 
FROM all_sessions --there are 266 distinct cities 
--further exploring the city column of all_sessions table
SELECT city, COUNT(*) AS count_city
FROM all_sessions
GROUP BY city
ORDER BY count_city DESC --There are 8302 records, where the city is not available in demo dataset
--and 354 records where city is '(not set)'
SELECT city, country
FROM all_sessions
WHERE city = '(not set)'
AND country = '(not set)' --this queries returns 23 records where both city and country are not set
--check for missing records
SELECT *
FROM all_sessions
WHERE city IS NULL

--use Sql CASE statement to impute data for instances where city is (not set) or not available in demo dataset
--after exploring the all sessions table, create a new all sessions table that's cleaned and suitable for analysis
CREATE TABLE all_sessions_cleaned AS
SELECT fullvisitorid,
       channelgrouping,
       pageviews,
       date,
       visitid,
       (productprice/1000000) AS productprice,
       productsku,
       v2productname,
       v2productcategory,
       CASE WHEN city = '(not set)' THEN country
            WHEN city = 'not available in demo dataset' THEN country
            WHEN city = '(not set)' AND country = '(not set)' THEN 'unknown'
            ELSE city
       END AS city,
       CASE WHEN country = '(not set)' THEN city
            WHEN country = '(not set)' AND city = '(not set)' THEN 'unknown'
            ELSE country
       END AS country
FROM (
    SELECT fullvisitorid,
           channelgrouping,
           pageviews,
           date,
           visitid,
           (productprice/1000000) AS productprice,
           productsku,
           v2productname,
           v2productcategory,
           CASE WHEN city = '(not set)' THEN country
                WHEN city = 'not available in demo dataset' THEN country
                WHEN city = '(not set)' AND country = '(not set)' THEN 'unknown'
                ELSE city
           END AS city,
           CASE WHEN country = '(not set)' THEN city
                WHEN country = '(not set)' AND city = '(not set)' THEN 'unknown'
                ELSE country
           END AS country,
           ROW_NUMBER() OVER (PARTITION BY fullvisitorid ORDER BY fullvisitorid) AS rn
    FROM all_sessions
) AS all_sessions_subquery
WHERE rn = 1;




