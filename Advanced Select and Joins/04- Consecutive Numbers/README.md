# 04- Consecutive Numbers

---

### Table: Logs

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| num         | varchar |

**Primary Key:** id  
**Description:**  
- `id` is an auto-increment column.  
- `num` represents the number associated with each log entry.

### Problem Statement

Find all numbers that appear at least three times consecutively.

Return the result table in any order.

### Example

**Input:**

| id | num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

**Output:**

| ConsecutiveNums |
|-----------------|
| 1               |

**Explanation:**
- The number 1 is the only number that appears consecutively for at least three times.

### Solution

```sql
SELECT DISTINCT a.num AS ConsecutiveNums 
FROM Logs a
JOIN Logs b
ON a.id = b.id - 1
JOIN Logs c
ON b.id = c.id - 1
WHERE a.num = b.num AND b.num = c.num;
```

---

