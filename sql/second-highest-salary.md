# Second Highest Salary

## Problem Statement
Find the second highest salary from the Employee table.

## MySQL Query
```sql
SELECT (SELECT DISTINCT salary 
        FROM Employee 
        ORDER BY salary DESC 
        LIMIT 1 OFFSET 1) AS SecondHighestSalary;
