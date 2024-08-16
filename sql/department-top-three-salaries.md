# Department Top Three Salaries

## Problem Statement
Find the top three highest salaries and their corresponding employees in each department.

## MySQL Query
```sql
WITH win_fun AS (
  SELECT e.id, 
         d.name AS Department, 
         e.name AS Employee, 
         salary AS Salary,
         DENSE_RANK() OVER (PARTITION BY d.name ORDER BY salary DESC) AS emp_rank
  FROM Employee e
  JOIN Department d ON e.departmentId = d.id
)
SELECT Department, Employee, Salary 
FROM win_fun
WHERE emp_rank <= 3
ORDER BY Department;


This query uses a Common Table Expression (CTE) with the `DENSE_RANK()` window function to rank salaries within each department and then selects the top three salaries.
