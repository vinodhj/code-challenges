
# LeetCode Problem: Combine Two Tables

## Problem Description
You are given two tables, `Person` and `Address`, with the following structure:

**Person**:
- `personId`: Primary key for this table.
- `firstName`: The first name of the person.
- `lastName`: The last name of the person.

**Address**:
- `addressId`: Primary key for this table.
- `personId`: Foreign key that links to the `Person` table.
- `city`: The city where the person lives.
- `state`: The state where the person lives.

Write a SQL query to select the first name, last name, city, and state of each person. The query should return all persons from the `Person` table and the corresponding city and state from the `Address` table. If a person does not have an address, still return their name with `NULL` values for `city` and `state`.

## SQL Query

```sql
SELECT Person.firstName, Person.lastName, Address.city, Address.state
FROM Person
LEFT JOIN Address ON Person.personId = Address.personId;
```

## Notes
- The `LEFT JOIN` ensures that all persons are included in the result, even if they don't have an address.
- The query is designed to handle cases where a person might not have a corresponding entry in the `Address` table.
