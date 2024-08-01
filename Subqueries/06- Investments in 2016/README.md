# 06- Investments in 2016

---

### Tables

**Insurance**

| Column Name | Type  |
|-------------|-------|
| pid         | int   |
| tiv_2015    | float |
| tiv_2016    | float |
| lat         | float |
| lon         | float |

### Problem Statement

Report the sum of all total investment values in 2016 (`tiv_2016`) for policyholders who:

1. Have the same `tiv_2015` value as one or more other policyholders.
2. Are not located in the same city as any other policyholder (i.e., the `(lat, lon)` attribute pairs must be unique).

The result should round `tiv_2016` to two decimal places.

### Example

**Input:**

**Insurance Table:**

| pid | tiv_2015 | tiv_2016 | lat | lon |
|-----|----------|----------|-----|-----|
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |

**Output:**

| tiv_2016 |
|----------|
| 45.00    |

**Explanation:**

- The first and fourth records meet both criteria. 
  - The `tiv_2015` value 10 is shared by the third and fourth records.
  - Their locations are unique.
- The second record does not meet either criterion. Its `tiv_2015` value is unique, and its location is not unique.
  
The result is the sum of `tiv_2016` for the first and last records, which is 45.

### Solution

```sql
WITH Ins_pos AS (
    SELECT pid, tiv_2015, tiv_2016, TO_CHAR(lat) || ',' || TO_CHAR(lon) AS pos
    FROM Insurance
),
rep_tiv AS (
    SELECT tiv_2015
    FROM Ins_pos
    GROUP BY tiv_2015
    HAVING COUNT(*) > 1
),
rep_pos AS (
    SELECT pos
    FROM Ins_pos
    GROUP BY pos
    HAVING COUNT(*) > 1
)

SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM Ins_pos
WHERE pos NOT IN (SELECT pos FROM rep_pos)
AND tiv_2015 IN (SELECT tiv_2015 FROM rep_tiv);
```

---

