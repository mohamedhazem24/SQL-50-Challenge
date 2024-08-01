# 05- Product Price at a Given Date

---

### Table: Products

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| new_price    | int     |
| change_date  | date    |

**Primary Key:** (product_id, change_date)  
**Description:**  
- `product_id` is the identifier for the product.  
- `new_price` is the updated price of the product.  
- `change_date` is the date when the price change took effect.

### Problem Statement

Write a solution to find the prices of all products on `2019-08-16`. Assume the price of all products before any change is 10.

Return the result table in any order.

### Example

**Input:**

| product_id | new_price | change_date |
|------------|-----------|-------------|
| 1          | 20        | 2019-08-14  |
| 2          | 50        | 2019-08-14  |
| 1          | 30        | 2019-08-15  |
| 1          | 35        | 2019-08-16  |
| 2          | 65        | 2019-08-17  |
| 3          | 20        | 2019-08-18  |

**Output:**

| product_id | price |
|------------|-------|
| 2          | 50    |
| 1          | 35    |
| 3          | 10    |

**Explanation:**
- For product 1, the price on `2019-08-16` is 35.
- For product 2, the price on `2019-08-16` is 50.
- For product 3, which has no price change before `2019-08-16`, the price remains 10.

### Solution

```sql
WITH LatestChanges AS (
    SELECT b.*
    FROM (
        SELECT product_id, MAX(change_date) AS change_date
        FROM Products
        WHERE change_date <= TO_DATE('2019-08-16', 'YYYY-MM-DD')
        GROUP BY product_id
    ) a
    LEFT JOIN Products b 
    ON a.product_id = b.product_id AND a.change_date = b.change_date
)
SELECT product_id, new_price AS price
FROM LatestChanges
UNION ALL
SELECT DISTINCT product_id, 10 AS price
FROM Products a
WHERE a.product_id NOT IN (SELECT product_id FROM LatestChanges);
```

---

