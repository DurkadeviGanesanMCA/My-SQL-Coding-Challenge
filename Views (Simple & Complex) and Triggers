Day 8: SQL Coding Challenge — Views (Simple & Complex) and Triggers

**Database:** `SQL_COMPANY_DB`  
**SQL Dialect:** MySQL
---

Question 1 — SIMPLE VIEW: `EmployeeBasicView`

**Scenario:**  
HR wants a quick view showing each employee’s name, department, and salary without accessing full details.

**Task:**  
Create a simple view named `EmployeeBasicView` that displays `EmpName`, `DeptID`, and `Salary` from the `Employees` table. Then, query the view to verify results.

**Answer:**
SQL Code:
CREATE OR REPLACE VIEW EmployeeBasicView AS
SELECT
    emp_name AS EmpName,
    dept_id  AS DeptID,
    salary   AS Salary
FROM Employees;

SELECT * FROM EmployeeBasicView;

---

Question 2 — COMPLEX VIEW: `EmployeeDepartmentView`

**Scenario:**  
Management needs a detailed view combining employee and department information.

**Task:**  
Create a complex view named `EmployeeDepartmentView` that joins `Employees` and `Departments` to show `EmpName`, `DeptName`, `Location`, and `Salary`.

**Answer:**
SQL Code:
CREAT VIEW EmployeeDepartmentView AS
SELECT
    e.emp_name AS EmpName,
    d.dept_name AS DeptName,
    e.city     AS Location,
    e.salary   AS Salary
FROM Employees e
LEFT JOIN Departments d
    ON e.dept_id = d.dept_id;

SELECT * FROM EmployeeDepartmentView;

---

Question 3 — COMPLEX VIEW WITH AGGREGATION: `DeptSalaryStats`

**Scenario:**  
The finance department wants to analyze average salary and employee count per department.

**Task:**  
Create a complex view named `DeptSalaryStats` that shows each department’s name, average salary, and number of employees.

**Answer:**
SQL Code:
CREATE VIEW DeptSalaryStats AS
SELECT
    d.dept_name AS DeptName,
    AVG(e.salary) AS AvgSalary,
    COUNT(e.emp_id) AS TotalEmployees
FROM Departments d
LEFT JOIN Employees e
    ON d.dept_id = e.dept_id
GROUP BY d.dept_name;

SELECT * FROM DeptSalaryStats;

---

Question 4 — UPDATE USING VIEW

**Scenario:**  
HR wants to increase salary by ₹5,000 for all employees visible in the view.

**Task:**  
Use `EmployeeBasicView` to update each employee’s salary by ₹5,000. Ensure the change reflects in the main `Employees` table.

**Answer:**
SQL Code:
UPDATE EmployeeBasicView
SET Salary = Salary + 5000;

SELECT emp_name AS EmpName, salary AS Updated_Salary
FROM Employees;

---

Question 5 — DROP VIEW

**Scenario:**  
After the financial analysis is complete, some views are no longer needed.

**Task:**  
Drop the `DeptSalaryStats` view from the database.

**Answer:**
SQL Code:
DROP VIEW IF EXISTS DeptSalaryStats;

SHOW FULL TABLES
WHERE Table_type = 'VIEW';

---

Question 6 — TRIGGER (BEFORE INSERT)

**Scenario:**  
HR wants to prevent inserting an employee with a salary below ₹30,000.

**Task:**  
Create a `BEFORE INSERT` trigger named `check_min_salary` on the `Employees` table to block any insert with `Salary < 30000`.

**Answer:**
SQL Code:
DELIMITER $$

CREATE TRIGGER check_min_salary
BEFORE INSERT ON Employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 30000 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary must be at least 30000';
    END IF;
END$$

DELIMITER ;

**Test Insert:**
SQL Code:
INSERT INTO Employees (emp_id, emp_name, dept_id, salary, city)
VALUES (111, 'Test User', 2, 25000, 'Chennai');

---

Question 7 — TRIGGER (AFTER INSERT — Audit Log)

**Scenario:**  
The admin team wants to keep a record every time a new employee is added.

**Task:**  
Create a new table `EmployeeAudit(EmpID, EmpName, Action, ActionDate)`. Then create an `AFTER INSERT` trigger named `log_employee_insert` to insert a record into `EmployeeAudit` whenever a new employee is added.

**Answer:**
SQL Code:
CREATE TABLE IF NOT EXISTS EmployeeAudit (
    EmpID INT,
    EmpName VARCHAR(50),
    Action VARCHAR(50),
    ActionDate DATETIME
);

DELIMITER $$

CREATE TRIGGER log_employee_insert
AFTER INSERT ON Employees
FOR EACH ROW
BEGIN
    INSERT INTO EmployeeAudit (EmpID, EmpName, Action, ActionDate)
    VALUES (NEW.emp_id, NEW.emp_name, 'INSERT', NOW());
END$$

DELIMITER ;

**Test Insert:**
SQL Code:
INSERT INTO Employees (emp_id, emp_name, dept_id, salary, city)
VALUES (111, 'New Employee', 1, 32000, 'Madurai');

SELECT * FROM EmployeeAudit;

---

Question 8 — TRIGGER (AFTER UPDATE — Salary Change Log)

**Scenario:**  
Finance wants to track salary changes for compliance.

**Task:**  
Create a table `SalaryLog(EmpID, OldSalary, NewSalary, ChangeDate)`. Then create an `AFTER UPDATE` trigger named `log_salary_change` that logs every time an employee’s salary is updated.

**Answer:**
SQL Code:
CREATE TABLE IF NOT EXISTS SalaryLog (
    EmpID INT,
    OldSalary DECIMAL(10,2),
    NewSalary DECIMAL(10,2),
    ChangeDate DATETIME
);

DELIMITER $$

CREATE TRIGGER log_salary_change
AFTER UPDATE ON Employees
FOR EACH ROW
BEGIN
    IF OLD.salary <> NEW.salary THEN
        INSERT INTO SalaryLog (EmpID, OldSalary, NewSalary, ChangeDate)
        VALUES (NEW.emp_id, OLD.salary, NEW.salary, NOW());
    END IF;
END$$

DELIMITER ;

**Test Update:**
SQL Code:
UPDATE Employees
SET salary = salary + 2000
WHERE emp_id = 101;

SELECT * FROM SalaryLog;

---

Question 9 — TRIGGER (BEFORE DELETE — Block Action)

**Scenario:**  
The HR policy restricts deleting employees from the IT department.

**Task:**  
Create a `BEFORE DELETE` trigger named `prevent_it_delete` that prevents deletion of employees where `DeptID` corresponds to the IT department.

**Answer:**
SQL Code:
DELIMITER $$

CREATE TRIGGER prevent_it_delete
BEFORE DELETE ON Employees
FOR EACH ROW
BEGIN
    IF OLD.dept_id = (
        SELECT dept_id
        FROM Departments
        WHERE dept_name = 'IT'
        LIMIT 1
    ) THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Cannot delete employees from IT department';
    END IF;
END$$

DELIMITER ;

**Test Delete:**
SQL Code:
DELETE FROM Employees
WHERE emp_id = 101;

---

Question 10 — TRIGGER (AFTER DELETE — Archive Record)

**Scenario:**  
When any employee leaves the company, HR wants their record saved in an archive table.

**Task:**  
Create a new table `EmployeeArchive(EmpID, EmpName, DeptID, Salary, ExitDate)`. Then create an `AFTER DELETE` trigger named `archive_deleted_employee` that automatically inserts the deleted record into `EmployeeArchive`.

**Answer:**
SQL Code:
CREATE TABLE IF NOT EXISTS EmployeeArchive (
    EmpID INT,
    EmpName VARCHAR(50),
    DeptID INT,
    Salary DECIMAL(10,2),
    ExitDate DATETIME
);

DELIMITER $$

CREATE TRIGGER archive_deleted_employee
AFTER DELETE ON Employees
FOR EACH ROW
BEGIN
    INSERT INTO EmployeeArchive (EmpID, EmpName, DeptID, Salary, ExitDate)
    VALUES (OLD.emp_id, OLD.emp_name, OLD.dept_id, OLD.salary, NOW());
END$$

DELIMITER ;

**Test Delete:**
SQL Code:
DELETE FROM Employees
WHERE emp_id = 103;

SELECT * FROM EmployeeArchive;

---
