# 04- Restaurant Growth

---

### Tables

**Customer**

| Column Name | Type    |
|-------------|---------|
| customer_id | int     |
| name        | varchar |
| visited_on  | date    |
| amount      | int     |

### Problem Statement

Compute the moving average of how much the customer paid in a seven-day window (i.e., current day + 6 days before). The `average_amount` should be rounded to two decimal places.

Return the result table ordered by `visited_on` in ascending order.

### Example

**Input:**

**Customer Table:**

| customer_id | name   | visited_on | amount |
|-------------|--------|------------|--------|
| 1           | Jhon   | 2019-01-01 | 100    |
| 2           | Daniel | 2019-01-02 | 110    |
| 3           | Jade   | 2019-01-03 | 120    |
| 4           | Khaled | 2019-01-04 | 130    |
| 5           | Winston| 2019-01-05 | 110    |
| 6           | Elvis  | 2019-01-06 | 140    |
| 7           | Anna   | 2019-01-07 | 150    |
| 8           | Maria  | 2019-01-08 | 80     |
| 9           | Jaze   | 2019-01-09 | 110    |
| 1           | Jhon   | 2019-01-10 | 130    |
| 3           | Jade   | 2019-01-10 | 150    |

**Output:**

| visited_on | amount | average_amount |
|------------|--------|----------------|
| 2019-01-07 | 860    | 122.86         |
| 2019-01-08 | 840    | 120.00         |
| 2019-01-09 | 840    | 120.00         |
| 2019-01-10 | 1000   | 142.86         |

**Explanation:**

1. For the date 2019-01-07, the moving average is calculated from 2019-01-01 to 2019-01-07 with an `average_amount` of (100 + 110 + 120 + 130 + 110 + 140 + 150)/7 = 122.86.
2. For the date 2019-01-08, the moving average is calculated from 2019-01-02 to 2019-01-08 with an `average_amount` of (110 + 120 + 130 + 110 + 140 + 150 + 80)/7 = 120.00.
3. For the date 2019-01-09, the moving average is calculated from 2019-01-03 to 2019-01-09 with an `average_amount` of (120 + 130 + 110 + 140 + 150 + 80 + 110)/7 = 120.00.
4. For the date 2019-01-10, the moving average is calculated from 2019-01-04 to 2019-01-10 with an `average_amount` of (130 + 110 + 140 + 150 + 80 + 110 + 130 + 150)/7 = 142.86.

### Solution

```sql
WITH quered_dates AS (
    SELECT visited_on, SUM(amount) AS amount
    FROM Customer 
    WHERE visited_on >= (SELECT MIN(visited_on) + 6 FROM Customer)
    GROUP BY visited_on
),
joined_dates AS (
    SELECT qd.visited_on, c.amount
    FROM quered_dates qd
    LEFT JOIN Customer c 
    ON qd.visited_on >= c.visited_on AND qd.visited_on - c.visited_on < 7
)
SELECT TO_CHAR(visited_on, 'YYYY-MM-DD') AS visited_on,
       SUM(amount) AS amount,
       ROUND(SUM(amount) / 7, 2) AS average_amount
FROM joined_dates
GROUP BY visited_on
ORDER BY visited_on ASC;
```

---

