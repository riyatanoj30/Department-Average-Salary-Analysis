# Employee Salary Analysis - SQL Assignment

## Overview
This project contains a SQL solution to analyze employee salaries across departments and identify departments with above-average salaries. The solution includes complete database setup, data insertion, and query execution.

## Problem Statement
Find the average salary of employees in each department, along with the department name and the number of employees in each department. However, only include departments where the average salary is higher than the overall average salary across all departments.

## Database Schema

### Tables
1. **Departments**
   - `DepartmentID` (INT, Primary Key)
   - `Name` (VARCHAR(50), NOT NULL)

2. **Employees**
   - `EmployeeID` (INT, Primary Key)
   - `Name` (VARCHAR(50), NOT NULL)
   - `DepartmentID` (INT, Foreign Key)
   - `Salary` (DECIMAL(10,2))

## Sample Data

### Departments
| DepartmentID | Name        |
|--------------|-------------|
| 1            | Marketing   |
| 2            | Research    |
| 3            | Development |

### Employees
| EmployeeID | Name               | DepartmentID | Salary    |
|------------|--------------------|--------------|-----------|
| 1          | John Doe           | 1            | 60000.00  |
| 2          | Jane Smith         | 1            | 70000.00  |
| 3          | Alice Johnson      | 1            | 65000.00  |
| 4          | Bob Brown          | 1            | 75000.00  |
| 5          | Charlie Wilson     | 1            | 80000.00  |
| 6          | Eva Lee            | 2            | 70000.00  |
| 7          | Michael Clark      | 2            | 75000.00  |
| 8          | Sarah Davis        | 2            | 80000.00  |
| 9          | Ryan Harris        | 2            | 85000.00  |
| 10         | Emily White        | 2            | 90000.00  |
| 11         | David Martinez     | 3            | 95000.00  |
| 12         | Jessica Taylor     | 3            | 100000.00 |
| 13         | William Rodriguez  | 3            | 105000.00 |

## Files Included

- `complete_database_setup.sql` - Complete SQL script with database creation, data insertion, and queries
- `README.md` - This documentation file

## How to Run

1. **Prerequisites**
   - MySQL Server installed and running
   - MySQL client or workbench
   - Appropriate database privileges

2. **Execute the Script**
   ```sql
   -- Run the complete_database_setup.sql file
   -- This will create the database, tables, insert data, and execute queries
   ```

3. **Alternative Step-by-Step Execution**
   ```sql
   -- Step 1: Create and use database
   CREATE DATABASE EmployeeManagement;
   USE EmployeeManagement;
   
   -- Step 2: Create tables (see full script)
   -- Step 3: Insert data (see full script)
   -- Step 4: Execute main query (see full script)
   ```

## Query Logic

The main query uses the following approach:

1. **JOIN**: Combines Employees and Departments tables
2. **GROUP BY**: Groups results by department
3. **AGGREGATE FUNCTIONS**: 
   - `AVG(Salary)` - Calculate average salary per department
   - `COUNT(EmployeeID)` - Count employees per department
4. **SUBQUERY**: Calculate overall average salary across all employees
5. **HAVING CLAUSE**: Filter departments where avg salary > overall average
6. **ORDER BY**: Sort results by average salary (descending)

## Expected Results

### Overall Statistics
- **Total Employees**: 13
- **Overall Average Salary**: $79,230.77
- **Departments**: 3

### Department Analysis
| Department  | Average Salary | Number of Employees | Above Overall Average? |
|-------------|----------------|---------------------|------------------------|
| Marketing   | $70,000.00     | 5                   | No                     |
| Research    | $80,000.00     | 5                   | Yes                    |
| Development | $100,000.00    | 3                   | Yes                    |

### Main Query Output
Only departments with above-average salaries:

| DepartmentName | AverageSalary | NumberOfEmployees |
|----------------|---------------|-------------------|
| Development    | 100000.00     | 3                 |
| Research       | 80000.00      | 5                 |

## Key SQL Concepts Demonstrated

- Database and table creation
- Primary and foreign key constraints
- Data insertion
- INNER JOIN operations
- Aggregate functions (AVG, COUNT)
- Subqueries
- GROUP BY and HAVING clauses
- Conditional filtering

## Notes

- The query uses `HAVING` instead of `WHERE` because we're filtering on an aggregate function result
- The subquery `(SELECT AVG(Salary) FROM Employees)` calculates the overall average dynamically
- Results are ordered by average salary in descending order
- All salary calculations maintain decimal precision

## Troubleshooting

**Common Issues:**
1. **Database doesn't exist**: Ensure you run the CREATE DATABASE statement first
2. **Foreign key constraint errors**: Make sure Departments table is created and populated before Employees
3. **No results returned**: Verify data was inserted correctly using the verification SELECT statements

**Verification Queries:**
```sql
-- Check if data was inserted correctly
SELECT COUNT(*) FROM Employees; -- Should return 13
SELECT COUNT(*) FROM Departments; -- Should return 3

-- Verify the overall average
SELECT AVG(Salary) FROM Employees; -- Should be around 79230.77
```