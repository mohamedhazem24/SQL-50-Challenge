# 01- Employees Whose Manager Left the Company

---

### Table: Employees

| Column Name  | Type    |
|--------------|---------|
| employee_id  | int     |
| name         | varchar |
| manager_id   | int     |
| salary       | int     |

**Description:**  
- `employee_id` is the unique identifier for each employee.
- `name` is the employee's name.
- `manager_id` refers to the ID of the employee's manager. It can be `NULL` if the employee does not have a manager.
- `salary` is the employee's salary.

### Problem Statement

Find the IDs of employees whose salary is strictly less than $30,000 and whose manager has left the company. When a manager leaves, their record is deleted from the `Employees` table, but employees who reported to that manager still have their `manager_id` set to the ID of the manager who left.

Return the result table ordered by `employee_id`.

### Example

**Input:**

**Employees Table:**

| employee_id | name      | manager_id | salary |
|-------------|-----------|------------|--------|
| 3           | Mila      | 9          | 60301  |
| 12          | Antonella | null       | 31000  |
| 13          | Emery     | null       | 67084  |
| 1           | Kalel     | 11         | 21241  |
| 9           | Mikaela   | null       | 50937  |
| 11          | Joziah    | 6          | 28485  |

**Output:**

| employee_id |
|-------------|
| 11          |

**Explanation:**  
- Employees with a salary less than $30,000 are: 1 (Kalel) and 11 (Joziah).
- Kalel's manager is employee 11, who is still in the company.
- Joziah's manager is employee 6, who has left the company because there's no record of employee 6 in the table.

### Solution

```sql
SELECT employee_id
FROM Employees
WHERE salary < 30000 
AND manager_id NOT IN (SELECT employee_id FROM Employees)
ORDER BY employee_id;
```

---
