# 06- Employee Bonus
## Problem Description

Given the `Employee` and `Bonus` tables, write a solution to report the name and bonus amount of each employee with a bonus less than 1000. If an employee does not have a bonus record, they should still be included in the results with a `null` bonus value.

### Table Schema

**Employee**

| Column Name | Type    |
|-------------|---------|
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |

- `empId` is the primary key.
- Each row represents an employee's ID, name, their supervisor's ID, and their salary.

**Bonus**

| Column Name | Type |
|-------------|------|
| empId       | int  |
| bonus       | int  |

- `empId` is the primary key and also a foreign key referring to `empId` in the `Employee` table.
- Each row represents an employee's ID and their respective bonus.

### Requirements

Return the `name` and `bonus` amount of each employee where the bonus is less than 1000. Employees without a bonus should have a `null` value for the bonus.

### Example

#### Input:

**Employee table:**

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

**Bonus table:**

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

#### Output:

| name | bonus |
|------|-------|
| Brad | null  |
| John | null  |
| Dan  | 500   |

**Explanation:**
- Brad has no bonus record.
- John has no bonus record.
- Dan's bonus is less than 1000.

### Solution

```sql
SELECT e.name,
       b.bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```