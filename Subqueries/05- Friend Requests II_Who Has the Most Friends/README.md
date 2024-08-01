# 05- Friend Requests II_Who Has the Most Friends

---

### Tables

**RequestAccepted**

| Column Name   | Type    |
|---------------|---------|
| requester_id  | int     |
| accepter_id   | int     |
| accept_date   | date    |

### Problem Statement

Find the person who has the most friends and the number of friends they have.

In the case of ties, the test cases are generated so that only one person will have the most friends.

### Example

**Input:**

**RequestAccepted Table:**

| requester_id | accepter_id | accept_date |
|--------------|-------------|-------------|
| 1            | 2           | 2016-06-03  |
| 1            | 3           | 2016-06-08  |
| 2            | 3           | 2016-06-08  |
| 3            | 4           | 2016-06-09  |

**Output:**

| id | num |
|----|-----|
| 3  | 3   |

**Explanation:**

The person with ID 3 has friends with people 1, 2, and 4, totaling three friends, which is the most among all others.

### Solution

```sql
WITH CombinedRequests AS (
    SELECT requester_id AS id
    FROM RequestAccepted
    UNION
    SELECT accepter_id AS id
    FROM RequestAccepted
),
RequestCounts AS (
    SELECT id, COUNT(*) AS num
    FROM CombinedRequests
    GROUP BY id
)
SELECT id, num
FROM RequestCounts
WHERE num = (SELECT MAX(num) FROM RequestCounts);
```

---

