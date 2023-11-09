Question 1: Find all duplicate records
SQL Query:

SELECT *
FROM all_sessions
WHERE (visitId, fullVisitorId, channelGrouping)
IN (
    SELECT visitId, fullVisitorId,  channelGrouping
    FROM all_sessions
    GROUP BY visitId, fullVisitorId,  channelGrouping
    HAVING COUNT(*) > 1
)

Question 2: Find the total number of unique visitors (fullVisitorID).

SQL Query:
SELECT COUNT(DISTINCT fullVisitorId) AS total_unique_visitors
FROM all_sessions

Question 3: Find each unique product viewed by each visitor.

SQL Query:
SELECT
    fullVisitorId,
    productSKU AS viewed_product
FROM all_sessions
WHERE productSKU IS NOT NULL
GROUP BY fullVisitorId, productSKU
