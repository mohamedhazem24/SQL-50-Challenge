# 03- Triangle Judgement
---

### Table: Triangle

| Column Name | Type |
|-------------|------|
| x           | int  |
| y           | int  |
| z           | int  |

**Primary Key:** (x, y, z)  
**Description:**  
- Each row of this table contains the lengths of three line segments.

### Problem Statement

Report for every three line segments whether they can form a triangle.

Return the result table in any order.

### Example

**Input:**

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

**Output:**

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

**Explanation:**
- For the first row, the line segments cannot form a triangle as the sum of any two sides is not greater than the third side.
- For the second row, the line segments can form a triangle as the sum of any two sides is greater than the third side.

### Solution

```sql
SELECT x, y, z,
       (CASE WHEN (x + y > z AND x + z > y AND y + z > x) THEN 'Yes' ELSE 'No' END) AS triangle
FROM Triangle;
```

---
