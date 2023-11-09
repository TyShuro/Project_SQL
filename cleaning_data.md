What issues will you address by cleaning the data?
1. Scaling Issue - In the analytics table the Unit_price column scaling will be resolved by dividing by 1000000
2. Addressing missing Value in total revenue by Calculating Total revenue by Multiplying Units sold with unit per price
3. Null or Missing values - I intend to check tables for null or missing values in various columns across tables to ensure completeness and accuracy of the dataset
4. Text Cleaning any columns that I intend to use
5. Normalization - normalize data were necessary to prevent redundancy and improve the database structure

Queries:
Below, provide the SQL queries you used to clean your data.

UPDATE analytics
SET unit_price = unit_price / 1000000
    revenue = unit_price*units_sold
***Renaming Date column***
ALTER TABLE all_sessions
RENAME COLUMN "date" TO update_date;

****Addressing Missing values in city column***

UPDATE all_sessions
SET city = CASE
    WHEN city IS NULL 
         OR city = '' 
         OR city = '(not set)' 
         OR city = 'not available in demo dataset' 
    THEN country || '_city'
    ELSE city
    END

***Update the "item_quantity" column to 0 if it is NULL***
UPDATE all_sessions
SET itemquantity = COALESCE(itemquantity, 0)


***Creating a new Products table with unique product SKUs while retaining all columns from "products"**
CREATE TABLE normalized_products AS
SELECT DISTINCT ON (product_sku) *
FROM products

***Creating a new all_sessions table with normalized data based on "fullvisitorid"***
CREATE TABLE normalized_all_sessions AS
SELECT DISTINCT ON (fullvisitorid) *
FROM all_sessions


**Update NULL values in the "revenue" column with 0 in the "analytics" table**
UPDATE analytics
SET revenue = COALESCE(revenue, 0)



