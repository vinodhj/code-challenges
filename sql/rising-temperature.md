# Rising Temperature

## Problem Statement
Find the IDs of records where the temperature is higher than the temperature recorded on the previous day.

## MySQL Query
```sql
SELECT id
FROM (
    SELECT *, 
           LAG(recordDate) OVER (ORDER BY recordDate) AS prev_recordDate,
           LAG(temperature) OVER (ORDER BY recordDate) AS prevTemp
    FROM Weather
) AS sub
WHERE DATE_SUB(recordDate, INTERVAL 1 DAY) = prev_recordDate 
      AND temperature > prevTemp;



This query uses the `LAG()` window function to get the previous record's date and temperature, and then filters for records where the temperature has risen compared to the previous day.
