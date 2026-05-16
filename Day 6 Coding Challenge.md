## StudentsDB SQL Project

```sql
-- =========================================
-- Create Database
-- =========================================

CREATE DATABASE StudentsDB;

USE StudentsDB;

-- =========================================
-- Create Tables
-- =========================================

CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50),
    Age INT,
    City VARCHAR(50)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(50),
    Duration VARCHAR(20)
);

CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,

    FOREIGN KEY (StudentID)
    REFERENCES Students(StudentID),

    FOREIGN KEY (CourseID)
    REFERENCES Courses(CourseID)
);

-- =========================================
-- Insert Sample Data
-- =========================================

INSERT INTO Students
VALUES
(1, 'Aarav', 21, 'Chennai'),
(2, 'Meera', 22, 'Bangalore'),
(3, 'Karthik', 23, 'Hyderabad'),
(4, 'Divya', 21, 'Delhi');

INSERT INTO Courses
VALUES
(101, 'Data Analytics', '3 Months'),
(102, 'Python Programming', '2 Months'),
(103, 'SQL Basics', '1 Month');

INSERT INTO Enrollments
VALUES
(1001, 1, 101, '2025-05-10'),
(1002, 2, 102, '2025-06-01'),
(1003, 3, 103, '2025-06-15');

-- =========================================
-- Display Tables
-- =========================================

SELECT * FROM Students;

SELECT * FROM Courses;

SELECT * FROM Enrollments;

-- =========================================
-- JOIN Queries
-- =========================================

-- Show students with their enrolled course names

SELECT
    S.StudentID,
    S.StudentName,
    C.CourseID,
    C.CourseName
FROM Students S
JOIN Enrollments E
ON S.StudentID = E.StudentID
JOIN Courses C
ON C.CourseID = E.CourseID;

-- =========================================
-- LEFT JOIN and RIGHT JOIN
-- =========================================

-- List all students and their courses using LEFT JOIN

SELECT
    S.StudentName,
    E.CourseID
FROM Students S
LEFT JOIN Enrollments E
ON S.StudentID = E.StudentID;

-- List all students and their courses using RIGHT JOIN

SELECT
    S.StudentName,
    E.CourseID
FROM Students S
RIGHT JOIN Enrollments E
ON S.StudentID = E.StudentID;

-- =========================================
-- Numeric Functions
-- =========================================

-- Round the value 123.4567 to two decimal places

SELECT ROUND(123.4567, 2) AS RoundedValue;

-- Convert negative number to positive

SELECT ABS(-15) AS Positive_Value;

-- Find remainder of 25 divided by 4

SELECT MOD(25, 4) AS Remainder;

-- =========================================
-- String Functions
-- =========================================

-- Combine student name and city

SELECT
    CONCAT(StudentName, ' From ', City, '.') AS Full_Description
FROM Students;

-- Find length of each student name

SELECT
    StudentName,
    LENGTH(StudentName) AS Name_Length
FROM Students;

-- Replace SQL with Database in course names

SELECT
    CourseName AS Course_Name,
    REPLACE(CourseName, 'SQL', 'Database') AS Updated_Course_Name
FROM Courses;

-- Generate code prefix using first 3 letters

SELECT
    StudentName,
    SUBSTRING(StudentName, 1, 3) AS Code_Prefix
FROM Students;

-- Show names in uppercase and lowercase

SELECT
    StudentName,
    UPPER(StudentName) AS Upper_Name,
    LOWER(StudentName) AS Lower_Name
FROM Students;

-- =========================================
-- Date Functions
-- =========================================

-- Display current date and time

SELECT NOW() AS Current_Date_And_Time;

-- Find number of days between two dates

SELECT
    DATEDIFF('2025-06-01', '2025-05-10') AS Days_Difference;

-- Add 10 days to EnrollmentDate

SELECT
    S.StudentName,
    E.EnrollmentDate,
    DATE_ADD(E.EnrollmentDate, INTERVAL 10 DAY) AS Follow_Up_Date
FROM Students S
JOIN Enrollments E
ON S.StudentID = E.StudentID;
```
