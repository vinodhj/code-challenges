# Customers Who Never Order

## Problem Statement
Find the names of customers from the Customers table who have never placed an order.

## MySQL Query
```sql
SELECT name AS Customers
FROM Customers c
LEFT OUTER JOIN Orders o ON c.id = o.customerId
WHERE o.id IS NULL;


This query uses a `LEFT OUTER JOIN` to include all customers and filter out those who do not have a corresponding entry in the Orders table.