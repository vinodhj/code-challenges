# Employee Bonus

## Problem Statement
Retrieve the names of employees and their bonuses. Include employees who do not have a bonus listed and display bonuses less than 1000.

## MySQL Query
```sql
SELECT e.name, 
       b.bonus
FROM Employee e
LEFT OUTER JOIN Bonus b ON e.empid = b.empid
WHERE b.bonus < 1000 OR b.bonus IS NULL;


This query performs a `LEFT OUTER JOIN` to include all employees and filter out those with bonuses less than 1000 or without a bonus.
