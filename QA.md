What are your risk areas? Identify and describe them.
Data Completeness: Ensuring that all required data fields are present and populated.
Data Accuracy: Validating the accuracy of data.
Data Duplicates: Identifying duplicate records.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

Data Completeness:

Check if there are any missing values in critical columns, such as "fullVisitorId," "visitId," or any other important fields.

SELECT
    COUNT(*) AS total_records,
    COUNT(fullVisitorId) AS non_null_fullVisitorId,
    COUNT(visitId) AS non_null_visitId
FROM all_sessions

Data Accuracy:

Check for unrealistic values or outliers in numeric columns like "transaction revenue" 
SELECT *
FROM all_sessions
WHERE transactionrevenue < 0


Data Duplicates:
Check for duplicate values on Unique identifiers

SELECT
    visitId,
    COUNT(*) AS duplicate_count
FROM all_sessions
GROUP BY visitId
HAVING COUNT(*) > 1

