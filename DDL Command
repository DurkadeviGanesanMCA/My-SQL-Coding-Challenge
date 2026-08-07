## Hospital Database SQL Operations

```sql
USE hospital;

-- TO Create a Table
CREATE TABLE Patients (
    PatientID INT,
    PatientName VARCHAR(50),
    Age INT,
    Gender VARCHAR(10),
    AdmissionDate DATE
);

-- ALTER – Add Column
ALTER TABLE Patients
ADD COLUMN DoctorAssigned VARCHAR(50);

-- ALTER – Modify Column
-- Scenario: Increase the length of PatientName from VARCHAR(50) to VARCHAR(100).

ALTER TABLE Patients
MODIFY PatientName VARCHAR(100);

-- RENAME Table
-- Rename the table Patients to Patients_info.

ALTER TABLE Patients
RENAME TO Patients_info;

-- TRUNCATE keeps the structure but clears data.
TRUNCATE TABLE Patients_info;

-- DROP removes the table completely.
DROP TABLE Patients_info;

-- Drop Database
DROP DATABASE hospital;
```
