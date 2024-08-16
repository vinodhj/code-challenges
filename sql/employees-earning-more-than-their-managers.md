# Employees Earning More Than Their Managers

## Problem Statement
Find the names of employees who earn more than their managers.

## MySQL Query
```sql
SELECT e.name AS Employee
FROM Employee e
INNER JOIN Employee m ON e.managerId = m.id
WHERE e.salary > m.salary;
