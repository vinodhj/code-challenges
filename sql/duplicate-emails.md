# Duplicate Emails

## Problem Statement
Find all emails from the Person table that appear more than once.

## MySQL Query
```sql
WITH rank_person AS (
  SELECT *, RANK() OVER (PARTITION BY email ORDER BY id) AS row_no
  FROM Person
)
SELECT email AS Email
FROM rank_person
WHERE row_no > 1
GROUP BY email;



This query uses a Common Table Expression (CTE) to rank rows partitioned by email and then selects emails where the rank is greater than 1, indicating duplicates.
