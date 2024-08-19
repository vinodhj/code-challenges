# Find Person with the Most Friends

## Table: RequestAccepted

| Column Name   | Type    |
|---------------|---------|
| requester_id  | int     |
| accepter_id   | int     |
| accept_date   | date    |

- **Primary Key:** `(requester_id, accepter_id)`
- This table contains the ID of the user who sent the friend request, the ID of the user who accepted the request, and the date when the request was accepted.

## Problem Description

Find the person who has the most friends and the number of friends they have. The test cases are generated so that only one person has the most friends.

## Example

### Input:

**RequestAccepted** table:

| requester_id | accepter_id | accept_date |
|--------------|-------------|-------------|
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |

### Output:

| id | num |
|----|-----|
| 3  | 3   |

### Explanation:

The person with ID 3 is friends with people 1, 2, and 4, so they have three friends in total, which is the most among all the users.

## SQL Query

```sql
WITH FriendCount AS (
    SELECT 
        id,
        COUNT(*) AS num
    FROM (
        SELECT requester_id AS id
        FROM RequestAccepted
        UNION ALL
        SELECT accepter_id AS id
        FROM RequestAccepted
    ) AS AllFriends
    GROUP BY id
)
SELECT * 
FROM FriendCount 
ORDER BY num DESC 
LIMIT 1;
