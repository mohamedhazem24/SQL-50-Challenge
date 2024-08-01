# 07- Department Top Three Salaries

---

### Tables

**Employee**

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| name          | varchar |
| salary        | int     |
| departmentId  | int     |

**Department**

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| name          | varchar |

### Problem Statement

Identify employees who are high earners in each department. A high earner in a department is defined as an employee whose salary is in the top three unique salaries for that department.

### Example

**Input:**

**Employee Table:**

| id | name  | salary | departmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |

**Department Table:**

| id | name  |
|----|-------|
| 1  | IT    |
| 2  | Sales |

**Output:**

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Joe      | 85000  |
| IT         | Randy    | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

**Explanation:**

- In the IT department:
  - Max earns the highest unique salary.
  - Both Randy and Joe earn the second-highest unique salary.
  - Will earns the third-highest unique salary.

- In the Sales department:
  - Henry earns the highest salary.
  - Sam earns the second-highest salary.
  - There is no third-highest salary as there are only two employees.

---
### Solution

```sql
SELECT department, employee, salary
FROM (
    SELECT
        d.name AS department,
        e.name AS employee,
        e.salary AS salary,
        DENSE_RANK() OVER (PARTITION BY d.name ORDER BY e.salary DESC) AS rnk
    FROM Employee e
    LEFT JOIN Department d ON e.departmentId = d.id
)
WHERE rnk <= 3;
```
