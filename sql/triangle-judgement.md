# Determine if Line Segments Form a Triangle

## Table: Triangle

| Column Name | Type |
|-------------|------|
| x           | int  |
| y           | int  |
| z           | int  |

- **Primary Key:** (x, y, z)
- Each row of this table contains the lengths of three line segments.

## Problem Description

For every three line segments `(x, y, z)`, determine whether they can form a triangle.

A set of three line segments can form a triangle if and only if the sum of any two sides is greater than the third side:
- `x + y > z`
- `x + z > y`
- `y + z > x`

## Example

### Input:

**Triangle** table:

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

### Output:

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

## SQL Query

```sql
SELECT x, y, z,
  CASE
    WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
    ELSE 'No'
  END AS triangle
FROM Triangle;
