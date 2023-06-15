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
WHERE table_name = 'all_sessions'
--returns column_name and data-type for all columns in all_sessions
```
