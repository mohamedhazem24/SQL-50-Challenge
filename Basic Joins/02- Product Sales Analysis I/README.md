# 02- Product Sales Analysis I
## Problem Description

Given two tables `Sales` and `Product`, the task is to report the `product_name`, `year`, and `price` for each `sale_id` in the `Sales` table.

### Table Schema

**Sales**

| Column Name | Type  |
|-------------|-------|
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |

- `(sale_id, year)` is the primary key for this table.
- `product_id` is a foreign key referencing the `Product` table.
- Each row shows a sale on the product identified by `product_id` in a certain year.

**Product**

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

- `product_id` is the primary key for this table.
- Each row indicates the name of the product.

### Requirements

Return the `product_name`, `year`, and `price` for each `sale_id` in the `Sales` table. The result can be returned in any order.

### Example

#### Input:

**Sales table:**

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

**Product table:**

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

#### Output:

| product_name | year | price |
|--------------|------|-------|
| Nokia        | 2008 | 5000  |
| Nokia        | 2009 | 5000  |
| Apple        | 2011 | 9000  |

**Explanation:** 
- For `sale_id = 1`, the product `Nokia` was sold for `5000` in `2008`.
- For `sale_id = 2`, the product `Nokia` was sold for `5000` in `2009`.
- For `sale_id = 7`, the product `Apple` was sold for `9000` in `2011`.

## Solution

```sql
SELECT p.product_name, s.year, s.price 
FROM Sales s
LEFT JOIN Product p ON s.product_id = p.product_id;
```