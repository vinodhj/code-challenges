# Salespersons Without Orders for Company "RED"

## Table: SalesPerson

| Column Name     | Type    |
|-----------------|---------|
| sales_id        | int     |
| name            | varchar |
| salary          | int     |
| commission_rate | int     |
| hire_date       | date    |

- **Primary Key:** `sales_id`
- Each row in this table represents a salesperson, including their ID, name, salary, commission rate, and hire date.

## Table: Company

| Column Name | Type    |
|-------------|---------|
| com_id      | int     |
| name        | varchar |
| city        | varchar |

- **Primary Key:** `com_id`
- Each row in this table represents a company, including its ID, name, and the city in which it is located.

## Table: Orders

| Column Name | Type |
|-------------|------|
| order_id    | int  |
| order_date  | date |
| com_id      | int  |
| sales_id    | int  |
| amount      | int  |

- **Primary Key:** `order_id`
- **Foreign Key:** `com_id` references `com_id` from the `Company` table.
- **Foreign Key:** `sales_id` references `sales_id` from the `SalesPerson` table.
- Each row in this table represents an order, including the ID of the company, the ID of the salesperson, the order date, and the amount paid.

## Problem Description

Find the names of all the salespersons who did not have any orders related to the company with the name **"RED"**.

## Example

### Input: 

**SalesPerson** table:

| sales_id | name | salary | commission_rate | hire_date  |
|----------|------|--------|-----------------|------------|
| 1        | John | 100000 | 6               | 4/1/2006   |
| 2        | Amy  | 12000  | 5               | 5/1/2010   |
| 3        | Mark | 65000  | 12              | 12/25/2008 |
| 4        | Pam  | 25000  | 25              | 1/1/2005   |
| 5        | Alex | 5000   | 10              | 2/3/2007   |

**Company** table:

| com_id | name   | city     |
|--------|--------|----------|
| 1      | RED    | Boston   |
| 2      | ORANGE | New York |
| 3      | YELLOW | Boston   |
| 4      | GREEN  | Austin   |

**Orders** table:

| order_id | order_date | com_id | sales_id | amount |
|----------|------------|--------|----------|--------|
| 1        | 1/1/2014   | 3      | 4        | 10000  |
| 2        | 2/1/2014   | 4      | 5        | 5000   |
| 3        | 3/1/2014   | 1      | 1        | 50000  |
| 4        | 4/1/2014   | 1      | 4        | 25000  |

### Output:

| name |
|------|
| Amy  |
| Mark |
| Alex |

### Explanation:

According to orders 3 and 4 in the `Orders` table, only salespersons John and Pam have sales to company "RED". Therefore, the result includes all other salespersons.

## SQL Query

```sql
SELECT name 
FROM SalesPerson 
WHERE sales_id NOT IN (
    SELECT o.sales_id 
    FROM Orders o 
    JOIN Company c 
    ON o.com_id = c.com_id 
    WHERE c.name = 'RED'
);
