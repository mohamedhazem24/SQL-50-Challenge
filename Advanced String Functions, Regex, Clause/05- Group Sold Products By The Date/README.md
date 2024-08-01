# 05- Group Sold Products By The Date


---

### Table: Activities

| Column Name | Type    |
|-------------|---------|
| sell_date   | date    |
| product     | varchar |

**Description:**  
- `sell_date` is the date on which the product was sold.
- `product` is the name of the product sold.

### Problem Statement

Find, for each date, the number of different products sold and their names. The sold product names for each date should be sorted lexicographically.

Return the result table ordered by `sell_date`.

### Example

**Input:**

| sell_date  | product     |
|------------|-------------|
| 2020-05-30 | Headphone   |
| 2020-06-01 | Pencil      |
| 2020-06-02 | Mask        |
| 2020-05-30 | Basketball  |
| 2020-06-01 | Bible       |
| 2020-06-02 | Mask        |
| 2020-05-30 | T-Shirt     |

**Output:**

| sell_date  | num_sold | products                     |
|------------|----------|------------------------------|
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |

**Explanation:**  
- For `2020-05-30`, the sold items are `Headphone`, `Basketball`, and `T-Shirt`. These are sorted lexicographically and separated by a comma.
- For `2020-06-01`, the sold items are `Pencil` and `Bible`. These are sorted lexicographically and separated by a comma.
- For `2020-06-02`, the sold item is `Mask`. It is listed alone.

### Solution

```sql
SELECT 
    TO_CHAR(sell_date, 'YYYY-MM-DD') AS sell_date,
    COUNT(DISTINCT product) AS num_sold,
    LISTAGG(product, ',') WITHIN GROUP (ORDER BY product) AS products
FROM Activities
GROUP BY sell_date
ORDER BY sell_date;
```

---
