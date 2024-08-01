# 04- Rising Temperature
## Problem Description

Given the table `Weather`, the task is to find all dates' IDs where the temperature was higher compared to the previous day's temperature.

### Table Schema

**Weather**

| Column Name  | Type    |
|--------------|---------|
| id           | int     |
| recordDate   | date    |
| temperature  | int     |

- `id` is the primary key for this table.
- Each row represents the temperature recorded on a specific date.
- There are no duplicate dates.

### Requirements

Return the IDs of the dates where the temperature was higher than the temperature on the previous day. The result can be returned in any order.

### Example

#### Input:

**Weather table:**

| id | recordDate | temperature |
|----|------------|-------------|
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |

#### Output:

| id |
|----|
| 2  |
| 4  |

**Explanation:**
- On 2015-01-02, the temperature (25) was higher than the previous day (10).
- On 2015-01-04, the temperature (30) was higher than the previous day (20).

## Solution

```sql
SELECT b.id
FROM Weather a
JOIN Weather b ON a.recordDate = b.recordDate - INTERVAL 1 DAY
WHERE b.temperature > a.temperature;
```