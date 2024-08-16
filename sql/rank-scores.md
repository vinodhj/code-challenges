# Rank Scores

## Problem Statement
Rank the scores from the Scores table in descending order.

## PostgreSQL Query
```sql
SELECT score, 
       DENSE_RANK() OVER (ORDER BY score DESC) AS rank 
FROM Scores;


This query uses the `DENSE_RANK()` window function to assign a rank to each score, with ranks ordered by the score in descending order.
