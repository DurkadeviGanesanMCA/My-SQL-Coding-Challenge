## ECommerceDB SQL Operations

```sql
-- =========================================
-- 1. Create Database
-- =========================================

CREATE DATABASE ECommerceDB;

USE ECommerceDB;

-- =========================================
-- 2. Create Product Table
-- =========================================

CREATE TABLE Product (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0)
);

-- =========================================
-- 3. Create Sales Table
-- =========================================

CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    quantity INT CHECK (quantity > 0),
    sale_amount DECIMAL(10,2) CHECK (sale_amount > 0),

    FOREIGN KEY (product_id)
    REFERENCES Product(product_id)
);

-- =========================================
-- 4. Insert Sample Data into Product Table
-- =========================================

INSERT INTO Product (product_id, product_name, price)
VALUES
(1, 'Laptop', 85000.00),
(2, 'Smartphone', 45000.00),
(3, 'Headphones', 5000.00),
(4, 'Keyboard', 1200.00),
(5, 'Mouse', 800.00),
(6, 'Monitor', 15000.00),
(7, 'Webcam', 3500.00);

-- =========================================
-- 5. Insert Sample Data into Sales Table
-- =========================================

INSERT INTO Sales (sale_id, product_id, quantity, sale_amount)
VALUES
(1, 1, 2, 170000.00),
(2, 2, 3, 135000.00),
(3, 3, 5, 25000.00),
(4, 4, 10, 12000.00),
(5, 5, 15, 12000.00),
(6, 6, 2, 30000.00),
(7, 7, 4, 14000.00);

-- =========================================
-- DISTINCT and ALIAS
-- =========================================

-- Display unique product names
SELECT DISTINCT(product_name)
FROM Product;

-- Display product names with alias ProductName
SELECT product_name AS ProductName
FROM Product;

-- Display unique product_id values from the Sales table
SELECT DISTINCT(product_id)
FROM Sales;

-- Display product price with alias Product_Price
SELECT price AS Product_Price
FROM Product;

-- =========================================
-- WHERE Clause Examples
-- =========================================

-- Display products whose price is greater than 10,000
SELECT price
FROM Product
WHERE price > 10000;

-- Display products whose price is less than 5,000
SELECT price
FROM Product
WHERE price < 5000;

-- Display sales where quantity equals 2
SELECT quantity
FROM Sales
WHERE quantity = 2;

-- Display products whose price is greater than or equal to 15,000
SELECT price
FROM Product
WHERE price >= 15000;

-- Display sales where quantity is not equal to 5
SELECT quantity
FROM Sales
WHERE quantity <> 5;

-- =========================================
-- Arithmetic Operations
-- =========================================

-- Display product name and price after 10% increase
SELECT
    product_name,
    price,
    price * 1.10 AS IncreasePrice
FROM Product;

-- Display sale amount and sale amount after adding 500
SELECT
    sale_amount,
    sale_amount + 500 AS TotalSales
FROM Sales;

-- =========================================
-- Logical Operators
-- =========================================

-- Display products whose price is greater than 5,000 AND less than 50,000
SELECT *
FROM Product
WHERE price > 5000
AND price < 50000;

-- Display sales where quantity is 2 OR 4
SELECT *
FROM Sales
WHERE quantity = 2
OR quantity = 4;

-- Display products whose price is NOT greater than 20,000
SELECT price
FROM Product
WHERE price <= 20000;

-- =========================================
-- NULL Conditions
-- =========================================

-- Display sales records where product_id is NULL
SELECT *
FROM Sales
WHERE product_id IS NULL;

-- Display products where price is NOT NULL
SELECT product_name, price
FROM Product
WHERE price IS NOT NULL;

-- =========================================
-- IN and NOT IN Operators
-- =========================================

-- Display products with product_id 1, 3, and 5
SELECT product_id, product_name, price
FROM Product
WHERE product_id IN (1, 3, 5);

-- Display products whose product_id is NOT 2, 4, and 6
SELECT product_id, product_name, price
FROM Product
WHERE product_id NOT IN (2, 4, 6);

-- =========================================
-- BETWEEN Operator
-- =========================================

-- Display products whose price is between 1,000 and 20,000
SELECT product_id, price
FROM Product
WHERE price BETWEEN 1000 AND 20000;

-- Display products whose price is NOT between 5,000 and 50,000
SELECT product_id, price
FROM Product
WHERE price NOT BETWEEN 5000 AND 50000;

-- =========================================
-- LIKE Operator
-- =========================================

-- Display products whose name starts with 'M'
SELECT product_name
FROM Product
WHERE product_name LIKE 'M%';

-- Display products whose name ends with 'e'
SELECT product_name
FROM Product
WHERE product_name LIKE '%e';

-- Display products whose name contains 'phone'
SELECT product_name
FROM Product
WHERE product_name LIKE '%phone%';

-- Display products whose name does not start with 'S'
SELECT product_name
FROM Product
WHERE product_name NOT LIKE 'S%';

-- =========================================
-- Combined Conditions
-- =========================================

-- Display products whose price is between 1,000 and 20,000
-- AND product name starts with 'M'

SELECT product_name, price
FROM Product
WHERE price BETWEEN 1000 AND 20000
AND product_name LIKE 'M%';

-- Display sales where quantity is between 2 and 10
SELECT *
FROM Sales
WHERE quantity BETWEEN 2 AND 10;

-- Display products whose product_id is in (1,2,3)
-- AND price greater than 5,000

SELECT product_id, price
FROM Product
WHERE product_id IN (1, 2, 3)
AND price > 5000;

-- =========================================
-- DISTINCT Example
-- =========================================

-- Display unique sale quantities from the Sales table
SELECT DISTINCT(quantity) AS UniqueSales
FROM Sales;
```
