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


```
