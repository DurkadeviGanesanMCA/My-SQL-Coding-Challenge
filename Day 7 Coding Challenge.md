## Employee Database SQL Subquery Examples

```sql
USE employee_database;

-- =========================================
-- Display Tables
-- =========================================

SELECT * FROM employees;

SELECT * FROM department;

SELECT * FROM location;

-- =========================================
-- Single Row Subquery Questions
-- =========================================

-- Find employees whose salary is greater than the average salary of all employees

SELECT Salary
FROM employees
WHERE Salary >
(
    SELECT AVG(Salary)
    FROM employees
);

-- Find employees who earn more than Reyansh Singh

SELECT Salary
FROM employees
WHERE Salary >
(
    SELECT Salary
    FROM employees
    WHERE Employee_name = 'Reyansh Singh'
);

-- Find employees who joined after Aarav Nair

SELECT hire_date
FROM employees
WHERE hire_date >
(
    SELECT hire_date
    FROM employees
    WHERE employee_name = 'Aarav Nair'
);

-- Find employees whose salary is greater than the average salary of the IT department

SELECT
    e.Salary,
    d.department_name
FROM employees e
JOIN department d
ON e.department_id = d.department_id
WHERE e.salary >
(
    SELECT AVG(e1.salary)
    FROM employees e1
    JOIN department d1
    ON e1.department_id = d1.department_id
    WHERE d1.department_name = 'IT'
);

-- Find employees whose performance rating is higher than the average performance rating of all employees

SELECT performance_rating
FROM employees
WHERE performance_rating >
(
    SELECT AVG(performance_rating)
    FROM employees
);

-- =========================================
-- Multi Row Subquery Questions
-- =========================================

-- Find employees who work in departments located in Pune

SELECT *
FROM employees
WHERE department_id IN
(
    SELECT department_id
    FROM department
    WHERE location_id IN
    (
        SELECT location_id
        FROM location
        WHERE location_name = 'Pune'
    )
);

-- Find employees whose salary is greater than any employee in the Marketing department

SELECT *
FROM employees
WHERE salary > ANY
(
    SELECT salary
    FROM employees
    WHERE department_id =
    (
        SELECT department_id
        FROM department
        WHERE department_name = 'Marketing'
    )
);

-- Find employees whose salary is greater than all employees in the Data Science department

SELECT *
FROM employees
WHERE salary > ALL
(
    SELECT salary
    FROM employees
    WHERE department_id =
    (
        SELECT department_id
        FROM department
        WHERE department_name = 'Data Science'
    )
);

-- Find employees who belong to departments that have employees with performance rating = 5

SELECT *
FROM employees
WHERE department_id IN
(
    SELECT department_id
    FROM employees
    WHERE performance_rating = 5
);

-- =========================================
-- Correlated Subquery Questions
-- =========================================

-- 1. Find employees whose salary is greater than the average salary of their department

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

-- 2. Find employees who earn the highest salary in their department

SELECT e.*
FROM employees e
WHERE e.salary =
(
    SELECT MAX(e1.salary)
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 3. Find employees whose performance rating is higher than the average performance rating in their department

SELECT e.*
FROM employees e
WHERE e.performance_rating >
(
    SELECT AVG(e1.performance_rating)
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 4. Find employees who joined after the average join date of their department

SELECT
    e.employee_name,
    e.hire_date
FROM employees e
WHERE e.hire_date >
(
    SELECT AVG(e1.hire_date)
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 5. Find employees whose salary is less than the maximum salary in their department

SELECT
    e.employee_name,
    e.salary
FROM employees e
WHERE e.salary <
(
    SELECT MAX(e1.salary)
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 6. Find employees whose salary is equal to the minimum salary in their department

SELECT
    e.employee_name,
    e.salary
FROM employees e
WHERE e.salary =
(
    SELECT MIN(e1.salary)
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 7. Find departments that have employees earning more than 70000

SELECT
    d.department_id,
    d.department_name
FROM department d
WHERE EXISTS
(
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
    AND e.salary > 70000
);

-- 8. Find employees whose salary is greater than at least one employee in their department

SELECT
    e.employee_name,
    e.salary
FROM employees e
WHERE e.salary > ANY
(
    SELECT e1.salary
    FROM employees e1
    WHERE e.department_id = e1.department_id
);

-- 9. Find employees who are the only employee in their department

SELECT
    e.employee_id,
    e.employee_name,
    e.department_id
FROM employees e
WHERE 1 =
(
    SELECT COUNT(*)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

-- 10. Find employees whose salary is greater than the average salary
-- of employees who joined after them

SELECT
    e.employee_name,
    e.salary
FROM employees e
WHERE e.salary >
(
    SELECT AVG(e1.salary)
    FROM employees e1
    WHERE e1.hire_date > e.hire_date
);
```
