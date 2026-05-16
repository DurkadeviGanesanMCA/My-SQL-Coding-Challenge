## Sales Analytics SQL Project

```sql
-- =========================================
-- Create Database
-- =========================================

CREATE DATABASE Sales_Analytics;

USE Sales_Analytics;

-- =========================================
-- 1. Customers Table
-- =========================================

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerName VARCHAR(100),
    Gender VARCHAR(10),
    City VARCHAR(50),
    Email VARCHAR(100)
);

INSERT INTO Customers (CustomerName, Gender, City, Email)
VALUES
('Arjun Kumar', 'Male', 'Chennai', 'arjun@gmail.com'),
('Priya Sharma', 'Female', 'Bangalore', 'priya@gmail.com'),
('John Mathew', 'Male', 'Mumbai', 'john@gmail.com'),
('Sneha Reddy', 'Female', 'Hyderabad', 'sneha@gmail.com'),
('Vikram Iyer', 'Male', 'Chennai', 'vikram@gmail.com'),
('Lakshmi Devi', 'Female', 'Coimbatore', 'lakshmi@gmail.com'),
('Rahul Verma', 'Male', 'Delhi', 'rahul@gmail.com'),
('Nisha Patel', 'Female', 'Ahmedabad', 'nisha@gmail.com'),
('Krishna Rao', 'Male', 'Hyderabad', 'krishna@gmail.com'),
('Ananya Gupta', 'Female', 'Pune', 'ananya@gmail.com'),
('Suresh Kumar', 'Male', 'Chennai', 'suresh@gmail.com'),
('Swati Singh', 'Female', 'Lucknow', 'swati@gmail.com'),
('Karan Malhotra', 'Male', 'Noida', 'karan@gmail.com'),
('Divya Menon', 'Female', 'Kochi', 'divya@gmail.com'),
('Amit Shah', 'Male', 'Surat', 'amit@gmail.com'),
('Pooja Mehta', 'Female', 'Mumbai', 'pooja@gmail.com'),
('Rajesh Nair', 'Male', 'Kerala', 'rajesh@gmail.com'),
('Harini Mohan', 'Female', 'Chennai', 'harini@gmail.com'),
('Rohit Singh', 'Male', 'Kanpur', 'rohit@gmail.com'),
('Meena Kumari', 'Female', 'Patna', 'meena@gmail.com'),
('Aditya Rao', 'Male', 'Hyderabad', 'aditya@gmail.com'),
('Neha Gupta', 'Female', 'Indore', 'neha@gmail.com'),
('Sameer Khan', 'Male', 'Bangalore', 'sameer@gmail.com'),
('Bhavana R', 'Female', 'Mysore', 'bhavana@gmail.com'),
('Raj Kumar', 'Male', 'Chennai', 'raj@gmail.com'),
('Sangeetha', 'Female', 'Bangalore', 'sangeetha@gmail.com'),
('Aravind', 'Male', 'Hyderabad', 'aravind@gmail.com'),
('Snehal', 'Female', 'Pune', 'snehal@gmail.com'),
('Joseph', 'Male', 'Kochi', 'joseph@gmail.com'),
('Maya', 'Female', 'Delhi', 'maya@gmail.com');

-- =========================================
-- 2. Products Table
-- =========================================

CREATE TABLE Products (
    ProductID INT PRIMARY KEY AUTO_INCREMENT,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10,2)
);

INSERT INTO Products (ProductName, Category, Price)
VALUES
('Laptop', 'Electronics', 55000),
('Headphones', 'Electronics', 2500),
('Office Chair', 'Furniture', 9000),
('Keyboard', 'Electronics', 1500),
('Mouse', 'Electronics', 800),
('Monitor', 'Electronics', 12000),
('Webcam', 'Electronics', 3000),
('Tablet', 'Electronics', 20000),
('Desk Lamp', 'Furniture', 1500),
('Standing Desk', 'Furniture', 18000),
('Bluetooth Speaker', 'Electronics', 3500),
('USB Hub', 'Electronics', 700),
('Printer', 'Electronics', 8500),
('Pen Drive 64GB', 'Electronics', 600),
('Router', 'Electronics', 2500);

-- =========================================
-- 3. Salespersons Table
-- =========================================

CREATE TABLE Salespersons (
    SalespersonID INT PRIMARY KEY AUTO_INCREMENT,
    SalespersonName VARCHAR(100),
    Region VARCHAR(50),
    TargetAmount DECIMAL(10,2)
);

INSERT INTO Salespersons (SalespersonName, Region, TargetAmount)
VALUES
('Meera', 'South', 300000),
('Rahul', 'North', 250000),
('Karthik', 'West', 200000),
('Neha', 'East', 180000);

-- =========================================
-- 4. Orders Table
-- =========================================

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    SalespersonID INT,
    ProductID INT,
    Quantity INT,
    OrderDate DATE,

    FOREIGN KEY (CustomerID)
    REFERENCES Customers(CustomerID),

    FOREIGN KEY (SalespersonID)
    REFERENCES Salespersons(SalespersonID),

    FOREIGN KEY (ProductID)
    REFERENCES Products(ProductID)
);

-- =========================================
-- Insert Sample Orders
-- =========================================

INSERT INTO Orders (CustomerID, SalespersonID, ProductID, Quantity, OrderDate)
VALUES
(1, 1, 1, 1, '2025-01-10'),
(2, 2, 3, 1, '2025-01-11'),
(3, 1, 4, 3, '2025-01-12'),
(4, 3, 1, 1, '2025-01-14'),
(5, 4, 2, 2, '2025-01-15'),
(6, 2, 6, 1, '2025-01-16'),
(1, 1, 2, 1, '2025-01-17'),
(3, 4, 5, 2, '2025-01-18'),
(2, 3, 1, 1, '2025-01-19'),
(4, 2, 3, 4, '2025-01-20'),
(5, 1, 6, 2, '2025-01-21'),
(6, 3, 4, 1, '2025-01-22'),
(1, 4, 5, 3, '2025-01-23'),
(2, 1, 2, 2, '2025-01-24'),
(3, 3, 6, 1, '2025-01-25'),
(4, 4, 4, 2, '2025-01-26'),
(5, 2, 1, 1, '2025-01-27'),
(6, 1, 3, 3, '2025-01-28'),
(1, 3, 6, 1, '2025-01-29'),
(2, 4, 5, 2, '2025-01-30');

-- =========================================
-- DISTINCT Queries
-- =========================================

-- List all distinct cities where customers live
SELECT DISTINCT(city) AS UniqueCity
FROM Customers;

-- Retrieve distinct product categories
SELECT DISTINCT(category)
FROM Products;

-- =========================================
-- Alias and Arithmetic Operations
-- =========================================

-- Display customer names and email IDs
SELECT
    CustomerName AS Customer_Name,
    Email AS Email_ID
FROM Customers;

-- Show product name, price, and double price
SELECT
    ProductName,
    Price,
    (Price * 2) AS DoublePrice
FROM Products;

-- Show product name and price after adding 10% tax
SELECT
    ProductName,
    Price * 1.10 AS PriceWithTax
FROM Products;

-- =========================================
-- WHERE Clause Examples
-- =========================================

-- Customers from Hyderabad
SELECT *
FROM Customers
WHERE City = 'Hyderabad';

-- Products priced above 10,000
SELECT *
FROM Products
WHERE Price > 10000;

-- Orders placed after 2025-01-12
SELECT *
FROM Orders
WHERE OrderDate > '2025-01-12';

-- Products whose price is not equal to 1500
SELECT Price
FROM Products
WHERE Price <> 1500;

-- Customers whose Email is NULL
SELECT CustomerName, Email
FROM Customers
WHERE Email IS NULL;

-- Orders where quantity is NOT NULL
SELECT *
FROM Orders
WHERE Quantity IS NOT NULL;

-- Female customers from Chennai
SELECT *
FROM Customers
WHERE Gender = 'Female'
AND City = 'Chennai';

-- =========================================
-- IN and NOT IN
-- =========================================

-- Customers from selected cities
SELECT *
FROM Customers
WHERE City IN ('Chennai', 'Bangalore', 'Hyderabad');

-- Products not in Electronics or Furniture
SELECT ProductName, Category
FROM Products
WHERE Category NOT IN ('Electronics', 'Furniture');

-- Products in Electronics or Furniture
SELECT ProductName, Category
FROM Products
WHERE Category IN ('Electronics', 'Furniture');

-- =========================================
-- ORDER BY and LIMIT
-- =========================================

-- Customers ordered by name
SELECT CustomerName
FROM Customers
ORDER BY CustomerName ASC;

-- Top 3 products by price
SELECT ProductName, Price
FROM Products
ORDER BY Price DESC
LIMIT 3;

-- Top 3 expensive products above 5000
SELECT ProductName, Price
FROM Products
WHERE Price > 5000
ORDER BY Price DESC
LIMIT 3;

-- =========================================
-- GROUP BY and HAVING
-- =========================================

-- Number of customers in each city
SELECT
    City,
    COUNT(*) AS CustomerCount
FROM Customers
GROUP BY City
ORDER BY CustomerCount DESC;

-- Customers from selected cities sorted by name
SELECT City, CustomerName
FROM Customers
WHERE City IN ('Chennai', 'Pune', 'Hyderabad')
ORDER BY CustomerName ASC;

-- Display city and customer name sorted
SELECT City, CustomerName
FROM Customers
ORDER BY City ASC, CustomerName ASC;

-- Customers whose name starts with A
SELECT CustomerName, CustomerID
FROM Customers
WHERE CustomerName LIKE 'A%'
ORDER BY CustomerID;

-- Total number of customers
SELECT COUNT(*) AS Total_Customers
FROM Customers;

-- Customers count by city
SELECT City, COUNT(*) AS Total_Customers
FROM Customers
GROUP BY City;

-- Customers count by gender
SELECT Gender, COUNT(*) AS Total_Customers
FROM Customers
GROUP BY Gender;

-- Group cities
SELECT City
FROM Customers
GROUP BY City;

-- Cities having customer count greater than 2
SELECT
    City,
    COUNT(CustomerID) AS Customer_Count
FROM Customers
GROUP BY City
HAVING Customer_Count > 2;

-- Orders count per order
SELECT
    OrderID,
    COUNT(*) AS Total_Orders
FROM Orders
GROUP BY OrderID
HAVING Total_Orders > 0;

-- Product quantity between 5 and 6
SELECT
    ProductID,
    SUM(Quantity) AS TotalQuantity
FROM Orders
GROUP BY ProductID
HAVING TotalQuantity BETWEEN 5 AND 6;

-- Average price by category above 5000
SELECT
    Category,
    AVG(Price) AS AveragePrice
FROM Products
GROUP BY Category
HAVING AveragePrice > 5000;

-- =========================================
-- JOINS
-- =========================================

-- Orders with customer names
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers C
JOIN Orders O
ON C.CustomerID = O.CustomerID;

-- Customers and orders using LEFT JOIN
SELECT
    C.*,
    O.OrderID
FROM Customers C
LEFT JOIN Orders O
ON C.CustomerID = O.CustomerID;

-- Salesperson names with orders using RIGHT JOIN
SELECT
    S.SalespersonName,
    O.OrderID
FROM Salespersons S
RIGHT JOIN Orders O
ON S.SalespersonID = O.SalespersonID;

-- Orders with customer and product details
SELECT
    O.OrderID,
    C.CustomerName,
    P.ProductName,
    O.Quantity,
    O.OrderDate
FROM Orders O
JOIN Customers C
ON O.CustomerID = C.CustomerID
JOIN Products P
ON O.ProductID = P.ProductID
ORDER BY O.OrderID;

-- Orders from Chennai customers
SELECT
    O.OrderID,
    C.CustomerName,
    C.City,
    P.ProductName,
    O.Quantity,
    O.OrderDate
FROM Orders O
JOIN Customers C
ON O.CustomerID = C.CustomerID
JOIN Products P
ON O.ProductID = P.ProductID
WHERE C.City = 'Chennai';

-- Customers who purchased Laptop
SELECT
    C.CustomerID,
    C.CustomerName
FROM Customers C
JOIN Orders O
ON C.CustomerID = O.CustomerID
JOIN Products P
ON O.ProductID = P.ProductID
WHERE P.ProductName = 'Laptop';

-- Total purchase amount for orders
SELECT
    O.OrderID,
    P.ProductName,
    O.Quantity,
    P.Price,
    (P.Price * O.Quantity) AS Total_Sales_Amount
FROM Orders O
JOIN Products P
ON O.ProductID = P.ProductID;
```
