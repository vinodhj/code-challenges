# Nth Highest Salary

## Problem Statement
Create a function to find the Nth highest salary from the Employee table.

## PostgreSQL Function
```sql
CREATE OR REPLACE FUNCTION NthHighestSalary(N INT) 
RETURNS TABLE (Salary INT) AS $$
BEGIN
  RETURN QUERY (
    WITH s_cte AS (
      SELECT e.salary AS n_salary, 
             DENSE_RANK() OVER (ORDER BY e.salary DESC) AS salary_rank
      FROM Employee e
    )
    SELECT n_salary
    FROM s_cte 
    WHERE salary_rank = N
    LIMIT 1
  );
END;
$$ LANGUAGE plpgsql;



This function uses a Common Table Expression (CTE) with `DENSE_RANK()` to rank salaries and then selects the salary with the rank matching the input parameter `N`.
