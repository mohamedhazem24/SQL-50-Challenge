# 01- Replace Employee ID With The Unique Identifier
## Problem Description

Given two tables `Employees` and `EmployeeUNI`, the task is to show the unique ID of each employee. If an employee does not have a unique ID, the result should show `null` for that employee.

### Table Schema

**Employees**

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

- `id` is the primary key for this table.
- Each row contains the `id` and `name` of an employee.

**EmployeeUNI**

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| unique_id   | int     |

- (id, unique_id) is the primary key for this table.
- Each row contains the `id` and the corresponding `unique_id` of an employee.

### Requirements

Return the `unique_id` of each employee. If an employee does not have a unique ID, return `null` for that employee. The result table can be returned in any order.

### Example

#### Input:

**Employees table:**

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

**EmployeeUNI table:**

| id | unique_id |
|----|-----------|
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

#### Output:

| unique_id | name     |
|-----------|----------|
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |

**Explanation:** 
- Alice and Bob do not have a unique ID, so `null` is shown for them.
- The unique ID of Meir is 2.
- The unique ID of Winston is 3.
- The unique ID of Jonathan is 1.

## Solution

```sql
SELECT u.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI u ON e.id = u.id;
```