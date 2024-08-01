# 01- Fix Names in a Table

---

### Table: Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| name        | varchar |

**Primary Key:** user_id  
**Description:**  
- `user_id` is the unique identifier for each user.
- `name` consists of the user's name, which can have mixed uppercase and lowercase characters.

### Problem Statement

Fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by `user_id`.

### Example

**Input:**

| user_id | name  |
|---------|-------|
| 1       | aLice |
| 2       | bOB   |

**Output:**

| user_id | name  |
|---------|-------|
| 1       | Alice |
| 2       | Bob   |

### Solution

```sql
SELECT 
    user_id, 
    CONCAT(UPPER(SUBSTR(name, 1, 1)), LOWER(SUBSTR(name, 2))) AS name 
FROM Users  
ORDER BY user_id;
```

---

