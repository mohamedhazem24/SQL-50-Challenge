# 04- Second Highest Salary

---

### Table: Employee

| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

**Primary Key:** id  
**Description:**  
- `id` is the unique identifier for each employee.
- `salary` represents the salary of the employee.

### Problem Statement

Find the second highest salary from the `Employee` table. If there is no second highest salary, return `NULL` (or `None` in Pandas).

### Example

**Input:**

| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

**Output:**

| SecondHighestSalary |
|---------------------|
| 200                 |

**Example 2:**

**Input:**

| id | salary |
|----|--------|
| 1  | 100    |

**Output:**

| SecondHighestSalary |
|---------------------|
| NULL                |

### Solution

```sql
SELECT MAX(salary) AS SecondHighestSalary 
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

---
