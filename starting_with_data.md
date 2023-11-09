Question 1: Which cities and countries have the highest level of transaction revenues on the site?

SQL Queries:

SELECT
    city,
    country,
    SUM(transactionRevenue) AS total_transaction_revenue
FROM
    all_sessions
WHERE
    transactionRevenue IS NOT NULL
GROUP BY
    city,
    country
ORDER BY
    total_transaction_revenue DESC

Answer: 

United States and the city of Sunnyvale


Question 2: What is the average number of products ordered from visitors in each city and country?

SQL Queries:


SELECT
    all_s.city,
    all_s.country,
    AVG(ps.orderedQuantity) AS average_products_ordered
FROM
    products ps
JOIN
    all_sessions all_s
On
    ps.productsku = all_s.productsku
Group by all_s.city,
    all_s.country
ORDER BY
    average_products_ordered DESC


Answer:
[data-1699554476110.csv](https://github.com/TyShuro/Project_SQL/files/13311604/data-1699554476110.csv)

Question 3:  Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?

SQL Queries:

SELECT
    city,
    country,
    v2ProductCategory AS product_category,
    COUNT(*) AS category_count
FROM
    all_sessions
WHERE
    v2ProductCategory IS NOT NULL  AND country != '(not set)'
GROUP BY
    city,
    country,
    v2ProductCategory
ORDER BY
    category_count DESC

Answer:
To identify patterns in the types (product categories) of products ordered from visitors in each city and country, I grouped the data by city, country, and product category and then counted the occurrences of each product category within each city and country. 

[dataQ3.csv](https://github.com/TyShuro/Project_SQL/files/13311685/dataQ3.csv)

Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
