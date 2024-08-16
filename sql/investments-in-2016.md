# Sum of Total Investment Values in 2016

## Problem Statement
Calculate the sum of all `tiv_2016` for policyholders who:
1. Have the same `tiv_2015` value as one or more other policyholders, and
2. Are not located in the same city as any other policyholder (i.e., the `(lat, lon)` attribute pairs must be unique).

Round the result to two decimal places.

## Example

### Input:
```text
+-----+----------+----------+-----+-----+
| pid | tiv_2015 | tiv_2016 | lat | lon |
+-----+----------+----------+-----+-----+
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |
+-----+----------+----------+-----+-----+

+----------+
| tiv_2016 |
+----------+
| 45.00    |
+----------+


```sql
SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM Insurance
WHERE tiv_2015 IN (
    SELECT tiv_2015
    FROM Insurance
    GROUP BY tiv_2015
    HAVING COUNT(*) > 1
)
AND (lat, lon) IN (
    SELECT lat, lon
    FROM Insurance
    GROUP BY lat, lon
    HAVING COUNT(*) = 1
);
```

This query calculates the sum of `tiv_2016` for policyholders who share the same `tiv_2015` with others but are uniquely located (i.e., their `(lat, lon)` coordinates are not shared with any other policyholders). The result is rounded to two decimal places.


