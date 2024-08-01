# 06- List the Products Ordered in a Period


---

### Table: Products

| Column Name      | Type    |
|------------------|---------|
| product_id       | int     |
| product_name     | varchar |
| product_category | varchar |

**Description:**  
- `product_id` is the unique identifier for each product.
- `product_name` is the name of the product.
- `product_category` is the category to which the product belongs.

### Table: Orders

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| order_date    | date    |
| unit          | int     |

**Description:**  
- `product_id` is a foreign key referencing the `Products` table.
- `order_date` is the date when the product was ordered.
- `unit` is the number of units ordered.

### Problem Statement

Write a solution to get the names of products that have at least 100 units ordered in February 2020 and their total amount.

Return the result table with product names and their ordered units, ordered by `product_name`.

### Example

**Input:**

**Products Table:**

| product_id | product_name          | product_category |
|------------|-----------------------|------------------|
| 1          | Leetcode Solutions    | Book             |
| 2          | Jewels of Stringology | Book             |
| 3          | HP                    | Laptop           |
| 4          | Lenovo                | Laptop           |
| 5          | Leetcode Kit          | T-shirt          |

**Orders Table:**

| product_id | order_date   | unit |
|------------|--------------|------|
| 1          | 2020-02-05   | 60   |
| 1          | 2020-02-10   | 70   |
| 2          | 2020-01-18   | 30   |
| 2          | 2020-02-11   | 80   |
| 3          | 2020-02-17   | 2    |
| 3          | 2020-02-24   | 3    |
| 4          | 2020-03-01   | 20   |
| 4          | 2020-03-04   | 30   |
| 4          | 2020-03-04   | 60   |
| 5          | 2020-02-25   | 50   |
| 5          | 2020-02-27   | 50   |
| 5          | 2020-03-01   | 50   |

**Output:**

| product_name       | unit |
|--------------------|------|
| Leetcode Solutions | 130  |
| Leetcode Kit       | 100  |

**Explanation:**  
- The product with `product_id = 1` was ordered a total of \(60 + 70 = 130\) units in February.
- The product with `product_id = 2` was ordered a total of 80 units in February.
- The product with `product_id = 3` was ordered a total of \(2 + 3 = 5\) units in February.
- The product with `product_id = 4` was not ordered in February.
- The product with `product_id = 5` was ordered a total of \(50 + 50 = 100\) units in February.

### Solution

```sql
SELECT p.product_name, gb.unit
FROM (
    SELECT product_id, SUM(unit) AS unit
    FROM Orders
    WHERE order_date BETWEEN TO_DATE('2020-02-01', 'YYYY-MM-DD') AND TO_DATE('2020-02-29', 'YYYY-MM-DD')
    GROUP BY product_id
) gb
LEFT JOIN Products p ON gb.product_id = p.product_id
WHERE gb.unit >= 100;
```

---

