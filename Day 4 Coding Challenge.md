## ECommerceDB SQL Aggregate and Ranking Queries

```sql
USE ECommerceDB;

-- =========================================
-- Top 3 Products by Price
-- =========================================

SELECT
    product_id,
    product_name,
    price
FROM Product
ORDER BY price DESC
LIMIT 3;

-- =========================================
-- COUNT() → Total Number of Sales Records
-- =========================================

SELECT
    COUNT(*) AS Total_Number_Of_Sales
FROM Sales;

-- =========================================
-- SUM() → Total Sales Amount
-- =========================================

SELECT
    SUM(sale_amount) AS Total_Sales
FROM Sales;

-- =========================================
-- AVG() → Average Sale Amount
-- =========================================

SELECT
    AVG(sale_amount) AS Average_Sales
FROM Sales;

-- =========================================
-- MAX() → Highest Sale Amount
-- =========================================

SELECT
    MAX(sale_amount) AS Maximum_Sales
FROM Sales;

-- =========================================
-- MIN() → Lowest Sale Amount
-- =========================================

SELECT
    MIN(sale_amount) AS Minimum_Sales
FROM Sales;

-- =========================================
-- Products with Total Sales Amount Greater Than 100
-- =========================================

SELECT
    product_id,
    SUM(sale_amount) AS Total_Sales
FROM Sales
GROUP BY product_id
HAVING Total_Sales > 100;

-- =========================================
-- Product Ranking Based on Price
-- =========================================

SELECT
    product_id,
    product_name,
    price,
    RANK() OVER (ORDER BY price DESC) AS Price_Rank
FROM Product;
```
