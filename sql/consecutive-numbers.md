# Consecutive Numbers

## Problem Statement
Find all numbers from the Logs table that appear in at least three consecutive rows.

## MySQL Query
```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs l1
JOIN Logs l2 ON l1.num = l2.num AND l1.id = l2.id - 1
JOIN Logs l3 ON l1.num = l3.num AND l2.id = l3.id - 1
ORDER BY ConsecutiveNums;


This query identifies numbers that appear in three consecutive rows by joining the table with itself twice. It then selects distinct numbers that meet the criteria.
