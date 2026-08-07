## BOOKSTORE Database SQL Operations

```sql
CREATE DATABASE BOOKSTORE;

USE BOOKSTORE;

-- =========================================
-- Question 1: CREATE TABLE with Constraints
-- =========================================

CREATE TABLE Books (
    BookID INTEGER PRIMARY KEY,
    Title VARCHAR(100) NOT NULL,
    Author VARCHAR(50) NOT NULL,
    ISBN VARCHAR(20) UNIQUE,
    Price DECIMAL(8,2) CHECK (Price > 0)
);

CREATE TABLE Orders (
    OrderID INTEGER PRIMARY KEY,
    BookID INTEGER,
    OrderDate DATE NOT NULL,
    Quantity INTEGER CHECK (Quantity > 0),

    FOREIGN KEY (BookID)
    REFERENCES Books(BookID)
);

-- =========================================
-- Question 2: ALTER TABLE – Add UNIQUE Constraint
-- =========================================

ALTER TABLE Books
ADD CONSTRAINT UQ_ISBN UNIQUE (ISBN);

-- =========================================
-- Question 3: INSERT, RETRIEVE & UPDATE
-- =========================================

-- Insert records into Books table

INSERT INTO Books (BookID, Title, Author, ISBN, Price)
VALUES
(1, 'SQL Basics', 'John Smith', 'ISBN001', 25.99),
(2, 'Database Design', 'Emily Clark', 'ISBN002', 40.50),
(3, 'Python for Data Analysis', 'Mark Lee', 'ISBN003', 35.75),
(4, 'Machine Learning Intro', 'Sarah Brown', 'ISBN004', 50.00),
(5, 'Advanced SQL Queries', 'David Miller', 'ISBN005', 45.25);

-- Insert records into Orders table

INSERT INTO Orders (OrderID, BookID, OrderDate, Quantity)
VALUES
(101, 1, '2026-05-10', 2),
(102, 3, '2026-05-11', 1),
(103, 5, '2026-05-12', 4);

-- Retrieve all records

SELECT * FROM Books;

SELECT * FROM Orders;

-- Update Price in Books table

UPDATE Books
SET Price = 30.99
WHERE BookID = 1;

-- Update Quantity in Orders table

UPDATE Orders
SET Quantity = 3
WHERE OrderID = 102;

-- Verify updates

SELECT * FROM Books;

SELECT * FROM Orders;

-- =========================================
-- Question 4: DELETE vs TRUNCATE
-- =========================================

-- DELETE specific row(s)

DELETE FROM Orders
WHERE OrderID = 103;

-- Verify remaining records

SELECT * FROM Orders;

-- TRUNCATE all rows from Orders table

TRUNCATE TABLE Orders;

-- Verify table is empty

SELECT * FROM Orders;
```
