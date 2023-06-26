What are your risk areas? Identify and describe them.
Data Validity
Syntax validation
logic validation
performance testing


QA Process:
Describe your QA process and include the SQL queries used to execute it.
```SQL
--Checking for duplicates in the allsessions table based on expected rows.
SELECT *
FROM all_sessions_cleaned --returns 14223 rows

SELECT DISTINCT fullvisitorid
FROM all_sessions_cleaned  --returns 14223 rows
--Confirmed that duplicates full visitor id have been removed from all_sessions table

--completeness in the country column of all_sessions cleaned
SELECT country, COUNT(*) AS count_country
FROM all_sessions_cleaned
WHERE country = '(not set)'
GROUP BY country
ORDER BY count_country DESC --returned 0 rows. to show that '(not set)' records in 
--the country column have been properly replaced