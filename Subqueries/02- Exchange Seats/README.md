# 02- Exchange Seats

---

### Table: Seat

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| student     | varchar |

**Description:**
- `id` is the primary key (unique value) column for this table.
- Each row represents a student with their `id` and `student` name.
- `id` is a continuous increment.

### Problem Statement

Swap the seat `id` of every two consecutive students. If the number of students is odd, the `id` of the last student should not be swapped.

Return the result table ordered by `id` in ascending order.

### Example

**Input:**

**Seat Table:**

| id | student |
|----|---------|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

**Output:**

| id | student |
|----|---------|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

**Explanation:**
- The seats are swapped as follows:
  - Students with `id` 1 and 2 are swapped.
  - Students with `id` 3 and 4 are swapped.
  - The last student with `id` 5 remains in place because the number of students is odd.

### Solution

```sql
SELECT 
    CASE 
        WHEN MOD(id, 2) = 0 THEN id - 1 
        ELSE id + 1 
    END AS id,
    student
FROM Seat
ORDER BY id;
```

---

