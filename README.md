## SQL Learning Journey Documentation

## Overview

This repository contains my hands-on SQL practice projects and query exercises completed as part of my learning journey in Database Management Systems and Data Analytics.

The projects cover:

- Database creation
- Table creation and constraints
- Data insertion and updates
- Filtering and sorting data
- Aggregate functions
- Grouping and ranking
- Joins
- Subqueries
- Correlated subqueries
- SQL functions
- Real-world business query scenarios

These SQL exercises were implemented using MySQL.

---

# SQL Concepts Covered

## 1. Database Operations

### Topics Practiced

- `CREATE DATABASE`
- `USE`
- `DROP DATABASE`
- `TRUNCATE TABLE`
- `DROP TABLE`

### Example

```sql
CREATE DATABASE BOOKSTORE;

USE BOOKSTORE;

DROP DATABASE BOOKSTORE;
```

---

## 2. Table Creation and Constraints

### Topics Practiced

- `PRIMARY KEY`
- `FOREIGN KEY`
- `UNIQUE`
- `CHECK`
- `NOT NULL`
- `AUTO_INCREMENT`

### Example

```sql
CREATE TABLE Books (
    BookID INTEGER PRIMARY KEY,
    Title VARCHAR(100) NOT NULL,
    Author VARCHAR(50) NOT NULL,
    ISBN VARCHAR(20) UNIQUE,
    Price DECIMAL(8,2) CHECK (Price > 0)
);
```

---

## 3. ALTER TABLE Operations

### Topics Practiced

- Add columns
- Modify columns
- Rename tables
- Add constraints

### Example

```sql
ALTER TABLE Patients
ADD COLUMN DoctorAssigned VARCHAR(50);

ALTER TABLE Patients
MODIFY PatientName VARCHAR(100);
```

---

# Projects Included

---

# 1. Hospital Database Project

## Concepts Covered

- Table creation
- ALTER operations
- RENAME table
- TRUNCATE table
- DROP table
- DROP database

## Sample Query

```sql
CREATE TABLE Patients (
    PatientID INT,
    PatientName VARCHAR(50),
    Age INT,
    Gender VARCHAR(10),
    AdmissionDate DATE
);
```

---

# 2. BOOKSTORE Database Project

## Concepts Covered

- Constraints
- INSERT statements
- UPDATE statements
- DELETE vs TRUNCATE
- Data retrieval

## Sample Query

```sql
INSERT INTO Books (BookID, Title, Author, ISBN, Price)
VALUES
(1, 'SQL Basics', 'John Smith', 'ISBN001', 25.99);
```

## Key Learnings

- How relational tables work
- Difference between DELETE and TRUNCATE
- How constraints maintain data integrity

---

# 3. ECommerceDB Project

## Concepts Covered

- DISTINCT
- ALIAS
- WHERE conditions
- Logical operators
- LIKE operator
- BETWEEN
- IN and NOT IN
- Arithmetic operations

## Sample Query

```sql
SELECT product_name,
       price,
       price * 1.10 AS IncreasePrice
FROM Product;
```

## Filtering Operations Practiced

```sql
SELECT *
FROM Product
WHERE price > 5000
AND price < 50000;
```

---

# 4. Aggregate and Ranking Queries

## Concepts Covered

- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`
- `GROUP BY`
- `HAVING`
- `RANK()`

## Sample Query

```sql
SELECT
    product_id,
    product_name,
    price,
    RANK() OVER (ORDER BY price DESC) AS Price_Rank
FROM Product;
```

## Key Learnings

- Business reporting queries
- Ranking products
- Aggregate calculations
- Data summarization

---

# 5. Sales Analytics Project

## Concepts Covered

- Multi-table relationships
- JOIN operations
- LEFT JOIN
- RIGHT JOIN
- GROUP BY and HAVING
- ORDER BY and LIMIT
- Business analytics queries

## Database Tables

- Customers
- Products
- Salespersons
- Orders

## Sample JOIN Query

```sql
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
ON O.ProductID = P.ProductID;
```

## Key Learnings

- Working with relational databases
- Connecting multiple tables
- Generating analytical reports
- Understanding sales analytics scenarios

---

# 6. StudentsDB Project

## Concepts Covered

- Student-course relationships
- SQL functions
- String functions
- Numeric functions
- Date functions
- JOIN operations

## Functions Practiced

### String Functions

- `CONCAT()`
- `LENGTH()`
- `REPLACE()`
- `SUBSTRING()`
- `UPPER()`
- `LOWER()`

### Numeric Functions

- `ROUND()`
- `ABS()`
- `MOD()`

### Date Functions

- `NOW()`
- `DATEDIFF()`
- `DATE_ADD()`

## Sample Query

```sql
SELECT
    StudentName,
    UPPER(StudentName) AS Upper_Name,
    LOWER(StudentName) AS Lower_Name
FROM Students;
```

---

# 7. Employee Database Subquery Project

## Concepts Covered

- Single-row subqueries
- Multi-row subqueries
- Correlated subqueries
- EXISTS
- ANY and ALL operators

## Subquery Types Practiced

### Single Row Subquery

```sql
SELECT Salary
FROM employees
WHERE Salary >
(
    SELECT AVG(Salary)
    FROM employees
);
```

### Correlated Subquery

```sql
SELECT
    e1.employee_name,
    e1.salary
FROM employees e1
WHERE e1.salary >
(
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e1.department_id = e2.department_id
);
```

## Key Learnings

- Advanced SQL querying
- Department-level analytics
- Employee performance analysis
- Nested query optimization concepts

---

# SQL Skills Practiced

| Category | Topics Covered |
|---|---|
| Database Operations | CREATE, DROP, USE |
| Table Operations | CREATE TABLE, ALTER TABLE |
| Constraints | PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK |
| Data Manipulation | INSERT, UPDATE, DELETE |
| Querying | SELECT, WHERE, DISTINCT |
| Sorting & Filtering | ORDER BY, LIMIT, BETWEEN, LIKE |
| Aggregations | COUNT, SUM, AVG, MIN, MAX |
| Grouping | GROUP BY, HAVING |
| Joins | INNER JOIN, LEFT JOIN, RIGHT JOIN |
| Functions | String, Numeric, Date Functions |
| Advanced SQL | Subqueries, Correlated Subqueries |
| Window Functions | RANK() |

---

# Tools Used

- MySQL
- MySQL Workbench
- GitHub
## Conclusion
This repository represents my SQL learning journey and practical hands-on experience with database
querying and analytics.
The projects demonstrate foundational to intermediate SQL concepts used in real-world data analytics and
business reporting scenarios
