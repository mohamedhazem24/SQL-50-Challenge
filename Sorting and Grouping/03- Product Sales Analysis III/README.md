# 03- Product Sales Analysis III


---

**Problem Statement**

Table: Sales

| Column Name | Type  |
|-------------|-------|
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |

`(sale_id, year)` is the primary key (combination of columns with unique values) of this table. `product_id` is a foreign key (reference column) to the Product table. Each row of this table shows a sale of the product `product_id` in a certain year. Note that the price is per unit.

Table: Product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

`product_id` is the primary key (column with unique values) of this table. Each row of this table indicates the product name of each product.

Write a solution to select the `product_id`, `year`, `quantity`, and `price` for the first year of every product sold.

Return the resulting table in any order.

**Example**

Input:
```
Sales table:
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+ 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+
Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+
```

Output:
```
+------------+------------+----------+-------+
| product_id | first_year | quantity | price |
+------------+------------+----------+-------+ 
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |
+------------+------------+----------+-------+
```

**Solution**

```sql
SELECT b.product_id AS product_id, b.year AS first_year, b.quantity AS quantity, b.price AS price 
FROM (SELECT s.product_id AS product_id, MIN(s.year) AS year
      FROM Sales s
      LEFT JOIN Product p ON s.product_id = p.product_id
      GROUP BY s.product_id) a
LEFT JOIN Sales b ON a.product_id = b.product_id AND a.year = b.year;
```

---

