# 07- Count Salary Categories


---

### Table: Accounts

| Column Name | Type |
|-------------|------|
| account_id  | int  |
| income      | int  |

**Primary Key:** account_id  
**Description:**  
- `account_id` is the unique identifier for each bank account.
- `income` represents the monthly income for the bank account.

### Problem Statement

Calculate the number of bank accounts for each salary category. The salary categories are:

- **Low Salary:** All the salaries strictly less than $20000.
- **Average Salary:** All the salaries in the inclusive range [$20000, $50000].
- **High Salary:** All the salaries strictly greater than $50000.

The result table must contain all three categories. If there are no accounts in a category, return 0.

Return the result table in any order.

### Example

**Input:**

| account_id | income |
|------------|--------|
| 3          | 108939 |
| 2          | 12747  |
| 8          | 87709  |
| 6          | 91796  |

**Output:**

| category       | accounts_count |
|----------------|----------------|
| Low Salary     | 1              |
| Average Salary | 0              |
| High Salary    | 3              |

**Explanation:**
- **Low Salary:** Account 2.
- **Average Salary:** No accounts.
- **High Salary:** Accounts 3, 6, and 8.

### Solution

```sql
SELECT 'Low Salary' AS category, COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income < 20000

UNION

SELECT 'Average Salary' AS category, COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income BETWEEN 20000 AND 50000

UNION

SELECT 'High Salary' AS category, COUNT(account_id) AS accounts_count
FROM Accounts
WHERE income > 50000;
```

---
