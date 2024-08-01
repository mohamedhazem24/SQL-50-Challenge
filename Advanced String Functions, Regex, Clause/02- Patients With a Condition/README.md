# 02- Patients With a Condition
---

### Table: Patients

| Column Name  | Type    |
|--------------|---------|
| patient_id   | int     |
| patient_name | varchar |
| conditions   | varchar |

**Primary Key:** patient_id  
**Description:**  
- `patient_id` is the unique identifier for each patient.
- `patient_name` is the name of the patient.
- `conditions` contains 0 or more codes separated by spaces. Type I Diabetes codes start with the prefix `DIAB1`.

### Problem Statement

Find the `patient_id`, `patient_name`, and `conditions` of the patients who have Type I Diabetes. Type I Diabetes codes always start with the prefix `DIAB1`.

Return the result table in any order.

### Example

**Input:**

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

**Output:**

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |

**Explanation:**
- Bob and George both have a condition that starts with `DIAB1`.

### Solution

```sql
SELECT *
FROM Patients
WHERE REGEXP_LIKE(conditions, '\bDIAB1\b');
```



---

