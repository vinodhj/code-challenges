# Department Highest Salary

## Problem Statement
Find the highest salary and the corresponding employee in each department.

## MySQL Query
```sql
WITH win_fun AS (
  SELECT e.id, 
         d.name AS Department, 
         e.name AS Employee, 
         MAX(salary) OVER (PARTITION BY d.name ORDER BY e.departmentId) AS salary,
         RANK() OVER (PARTITION BY d.name ORDER BY salary DESC) AS emp_rank
  FROM Employee e
  JOIN Department d ON e.departmentId = d.id
)
SELECT Department, Employee, salary 
FROM win_fun
WHERE emp_rank = 1
ORDER BY id;



This query uses a Common Table Expression (CTE) with window functions to partition the data by department and rank the salaries. It then selects the highest salary in each department.