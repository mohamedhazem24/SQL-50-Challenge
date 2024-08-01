# 03- Delete Duplicate Emails

---

### Table: Person

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| email       | varchar |

**Primary Key:** id  
**Description:**  
- `id` is the unique identifier for each person.
- `email` contains the email address of the person, and it will not contain uppercase letters.

### Problem Statement

Delete all duplicate emails, keeping only one unique email with the smallest `id`.

**Note:**  
- For SQL users, you are required to write a `DELETE` statement.
- For Pandas users, you are required to modify the `Person` DataFrame in place.

After running your script, the answer shown is the `Person` table. The driver will first compile and run your piece of code and then show the `Person` table. The final order of the `Person` table does not matter.

### Example

**Input:**

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

**Output:**

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |

**Explanation:**  
- `john@example.com` is repeated. Keep the row with the smallest `id` = 1.

### Solution

```sql
DELETE FROM Person
WHERE id NOT IN (
    SELECT MIN(id)
    FROM Person
    GROUP BY email
);
```

---
