# LeetCode SQL Problem: Monthly Transactions I

## Problem Description

You are given a table named `Transactions`:

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| country       | varchar |
| state         | enum    |
| amount        | int     |
| trans_date    | date    |
+---------------+---------+
```

- id is the primary key of this table.
- The table has information about incoming transactions.
- The state column is an enum of type ["approved", "declined"].

Write an SQL query to find for each month and country:
1. The number of transactions
2. Their total amount
3. The number of approved transactions
4. The total amount of approved transactions

Return the result table in any order.

### Example 1:

**Input:** 
Transactions table:
```
+------+---------+----------+--------+------------+
| id   | country | state    | amount | trans_date |
+------+---------+----------+--------+------------+
| 121  | US      | approved | 1000   | 2018-12-18 |
| 122  | US      | declined | 2000   | 2018-12-19 |
| 123  | US      | approved | 2000   | 2019-01-01 |
| 124  | DE      | approved | 2000   | 2019-01-07 |
+------+---------+----------+--------+------------+
```

**Output:** 
```
+----------+---------+-------------+----------------+--------------------+-----------------------+
| month    | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
+----------+---------+-------------+----------------+--------------------+-----------------------+
| 2018-12  | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01  | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01  | DE      | 1           | 1              | 2000               | 2000                  |
+----------+---------+-------------+----------------+--------------------+-----------------------+
```

## Solution

```sql
/* Write your PL/SQL query statement below*/
SELECT
    TO_CHAR(TO_DATE(MONTH, 'YYYY-MM-DD HH24:MI:SS'), 'YYYY-MM') AS month,
    COUNTRY,
    TRANS_COUNT,
    APPROVED_COUNT,
    TRANS_TOTAL_AMOUNT,
    APPROVED_TOTAL_AMOUNT
FROM  (SELECT TRUNC(trans_date, 'MM') as month
    ,country as country
    ,COUNT(*) as trans_count
    ,SUM(CASE WHEN state='approved' THEN 1 ELSE 0 END ) as approved_count
    ,SUM(amount) as trans_total_amount
    ,SUM(CASE WHEN state='approved' THEN amount ELSE 0 END ) as approved_total_amount
FROM Transactions
GROUP BY TRUNC(trans_date, 'MM'),country);
```

