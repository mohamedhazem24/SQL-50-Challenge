# 02- Primary Department for Each Employee

---

### Table: Employee

| Column Name   | Type    |
|---------------|---------|
| employee_id   | int     |
| department_id | int     |
| primary_flag  | varchar |

**Primary Key:** (employee_id, department_id)  
**Description:**  
- `employee_id` is the id of the employee.  
- `department_id` is the id of the department to which the employee belongs.  
- `primary_flag` is an ENUM ('Y', 'N'). If the flag is 'Y', the department is the primary department for the employee. If the flag is 'N', the department is not the primary.  

**Note:** Employees can belong to multiple departments. When an employee joins other departments, they need to decide which department is their primary department. If an employee belongs to only one department, their primary flag is 'N'.

### Problem Statement

Report all the employees with their primary department. For employees who belong to only one department, report their only department.

Return the result table in any order.

### Example

**Input:**

| employee_id | department_id | primary_flag |
|-------------|---------------|--------------|
| 1           | 1             | N            |
| 2           | 1             | Y            |
| 2           | 2             | N            |
| 3           | 3             | N            |
| 4           | 2             | N            |
| 4           | 3             | Y            |
| 4           | 4             | N            |

**Output:**

| employee_id | department_id |
|-------------|---------------|
| 1           | 1             |
| 2           | 1             |
| 3           | 3             |
| 4           | 3             |

**Explanation:**
- The primary department for employee 1 is 1.
- The primary department for employee 2 is 1.
- The primary department for employee 3 is 3.
- The primary department for employee 4 is 3.

### Solution

```sql
SELECT a.employee_id, b.department_id
FROM
(
    SELECT EMPLOYEE_ID AS EMPLOYEE_ID, MAX(primary_flag) AS prim_flag, COUNT(department_id) AS dept_count
    FROM Employee 
    GROUP BY EMPLOYEE_ID
    HAVING MAX(primary_flag) = 'Y' OR (MAX(primary_flag) = 'N' AND COUNT(department_id) = 1)
) a
LEFT JOIN Employee b 
ON a.EMPLOYEE_ID = b.EMPLOYEE_ID AND a.prim_flag = b.primary_flag;
```



