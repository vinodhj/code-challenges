# Find Managers with At Least Five Direct Reports

## Table: Employee

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

- **Primary Key:** `id`
- Each row of this table indicates the name of an employee, their department, and the ID of their manager.
- If `managerId` is `NULL`, then the employee does not have a manager.
- No employee will be the manager of themselves.

## Problem Description

Write a solution to find managers who have at least five direct reports.

## Example

### Input:

**Employee** table:

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

### Output:

| name |
|------|
| John |

### Explanation:

John (ID 101) is the manager of five employees (Dan, James, Amy, Anne, and Ron). Therefore, John's name is returned in the result.

## SQL Query

```sql
WITH temp1 AS (
    SELECT managerId
    FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING COUNT(*) > 4
),
temp2 AS (
    SELECT e.name 
    FROM Employee e 
    JOIN temp1 t 
    ON e.id = t.managerId
)
SELECT * FROM temp2;
