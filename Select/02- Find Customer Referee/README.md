# 02- Find Customer Referee

## Problem Description

Given a table `Customer`, the task is to find the names of customers that are not referred by the customer with `id = 2`.

### Table Schema

**Customer**

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

- `id` is the primary key column for this table.
- Each row indicates the id of a customer, their name, and the id of the customer who referred them.

### Requirements

- Return the names of the customers who are not referred by the customer with `id = 2`.
- The result table can be returned in any order.

### Example

#### Input:

**Customer table:**

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

#### Output:

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

## Solution

```sql
/* Write your PL/SQL query statement below */
SELECT name 
FROM Customer 
WHERE referee_id != 2 OR referee_id IS null;
```

---