# 03- Customer Who Visited but Did Not Make Any
## Problem Description

Given two tables, `Visits` and `Transactions`, the task is to find the IDs of customers who visited the mall without making any transactions and count the number of such visits for each customer.

### Table Schema

**Visits**

| Column Name | Type    |
|-------------|---------|
| visit_id    | int     |
| customer_id | int     |

- `visit_id` is the primary key for this table.
- This table contains information about the customers who visited the mall.

**Transactions**

| Column Name    | Type    |
|----------------|---------|
| transaction_id | int     |
| visit_id       | int     |
| amount         | int     |

- `transaction_id` is the primary key for this table.
- This table contains information about transactions made during each visit.

### Requirements

Return the IDs of the customers who visited the mall without making any transactions and the number of times they made such visits. The result table can be returned in any order.

### Example

#### Input:

**Visits table:**

| visit_id | customer_id |
|----------|-------------|
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

**Transactions table:**

| transaction_id | visit_id | amount |
|----------------|----------|--------|
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |

#### Output:

| customer_id | count_no_trans |
|-------------|----------------|
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |

**Explanation:** 
- Customer with ID 23 visited the mall once and made one transaction.
- Customer with ID 9 visited the mall once and made one transaction.
- Customer with ID 30 visited the mall once and did not make any transactions.
- Customer with ID 54 visited the mall three times; during two visits, they did not make any transactions.
- Customer with ID 96 visited the mall once and did not make any transactions.

## Solution

```sql
SELECT v.customer_id, COUNT(v.visit_id) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t ON v.visit_id = t.visit_id
WHERE t.visit_id IS NULL
GROUP BY v.customer_id;
```