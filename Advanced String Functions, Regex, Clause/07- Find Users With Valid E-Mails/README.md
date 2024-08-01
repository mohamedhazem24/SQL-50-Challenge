# 07- Find Users With Valid E-Mails

---

### Table: Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| name        | varchar |
| mail        | varchar |

**Description:**  
- `user_id` is the unique identifier for each user.
- `name` is the name of the user.
- `mail` is the email address of the user. Some emails may be invalid.

### Problem Statement

Write a solution to find users with valid emails. 

A valid email must:
- Start with a letter (either uppercase or lowercase).
- The prefix name can include letters, digits, underscores (`_`), periods (`.`), and/or dashes (`-`).
- End with `@leetcode.com`.

### Example

**Input:**

**Users Table:**

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

**Output:**

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |

**Explanation:**  
- User 2's email does not have a valid domain.
- User 5's email contains an invalid character (`#`).
- User 6's email has a domain other than `leetcode.com`.
- User 7's email starts with a period, which is invalid.

### Solution

```sql
SELECT *
FROM Users
WHERE REGEXP_LIKE(mail, '^[a-zA-Z][a-zA-Z0-9._-]*@leetcode\.com$');
```

---

