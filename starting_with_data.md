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

Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?

SQL Queries:
To find the top-selling product from each city and country and identify any notable patterns in the products sold, i used the "product" and "all_sessions" tables. I then grouped the data by city, country, and product SKU, calculated the total quantity sold for each product in each location, and then found the product with the highest sales in each city/country combination using order by 

WITH CityCountryProductSales AS (
    SELECT
        a.city,
        a.country,
	    a.v2ProductName,
        p.productSKU AS top_selling_product,
        SUM(p.orderedQuantity) AS total_quantity_sold
    FROM
        all_sessions a
    JOIN
        products p ON a.productSKU = p.productSKU
    WHERE
        p.orderedQuantity IS NOT NULL
    GROUP BY
        a.city,
        a.country,
        p.productSKU,
	    a.v2ProductName
)
SELECT
    ccp.city,
    ccp.country,
    ccp.top_selling_product,
    ccp.v2ProductName,
    ccp.total_quantity_sold
FROM
    CityCountryProductSales ccp
JOIN
    products p ON ccp.top_selling_product = p.productSKU
WHERE
    ccp.v2ProductName IS NOT NULL
    AND ccp.total_quantity_sold = (
        SELECT MAX(total_quantity_sold)
        FROM CityCountryProductSales
        WHERE city = ccp.city AND country = ccp.country
    )
	AND country != '(not set)'
ORDER BY
    ccp.city,
    ccp.country

Answer:
[dataQ4.csv](https://github.com/TyShuro/Project_SQL/files/13311794/dataQ4.csv)



Question 5: Can we summarize the impact of revenue generated from each city/country?

SQL Queries:


SELECT
    a.city,
    a.country,
    SUM(analytics.revenue) AS total_revenue_generated
FROM
    all_sessions a
JOIN
    analytics ON a.visitId = analytics.visitId
WHERE
    analytics.revenue IS NOT NULL
GROUP BY
    a.city,
    a.country
ORDER BY
    total_revenue_generated DESC

Answer:
To summarize the impact of revenue generated from each city/country I joined the "analytics" and "all_sessions" tables, and then calculated the total revenue for each city and country combination. 

[dataQ5.csv](https://github.com/TyShuro/Project_SQL/files/13311871/dataQ5.csv)



