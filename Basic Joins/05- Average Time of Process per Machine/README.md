# 05- Average Time of Process per Machine
## Problem Description

Given the `Activity` table, the task is to calculate the average time each machine takes to complete a process. The time to complete a process is the difference between the 'end' and 'start' timestamps for each process. The average time should be rounded to 3 decimal places.

### Table Schema

**Activity**

| Column Name    | Type    |
|----------------|---------|
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |

- `(machine_id, process_id, activity_type)` is the primary key for this table.
- `machine_id` is the ID of a machine.
- `process_id` is the ID of a process running on the machine with `machine_id`.
- `activity_type` indicates whether the activity is a 'start' or 'end' of a process.
- `timestamp` represents the current time in seconds.

### Requirements

Return the `machine_id` and the average time (`processing_time`) it takes for each machine to complete a process. The average time should be rounded to 3 decimal places.

### Example

#### Input:

**Activity table:**

| machine_id | process_id | activity_type | timestamp |
|------------|------------|---------------|-----------|
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     |
| 2          | 1          | end           | 5.000     |

#### Output:

| machine_id | processing_time |
|------------|-----------------|
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |

**Explanation:**
- Machine 0's average time is ((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894
- Machine 1's average time is ((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995
- Machine 2's average time is ((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456

## Solution

```sql
SELECT machine_id,
       ROUND(AVG(end_time - start_time), 3) AS processing_time
FROM (
    SELECT a.machine_id,
           a.timestamp AS start_time,
           b.timestamp AS end_time
    FROM Activity a
    JOIN Activity b
    ON a.machine_id = b.machine_id
    AND a.process_id = b.process_id
    AND a.activity_type = 'start'
    AND b.activity_type = 'end'
) AS times
GROUP BY machine_id;
```