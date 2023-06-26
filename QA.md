What are your risk areas? Identify and describe them.
Data Validity
Syntax validation
logic validation
performance testing


QA Process:
Describe your QA process and include the SQL queries used to execute it.
```SQL
--Checking for duplicates in the allsessions table.
SELECT *
FROM all_sessions_cleaned --returns 14223 rows

SELECT DISTINCT fullvisitorid
FROM all_sessions_cleaned  --returns 14223 rows
--Confirmed that duplicates full visitor id have been removed from all_sessions table
