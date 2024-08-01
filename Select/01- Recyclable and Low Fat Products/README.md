# 01- Recyclable and Low Fat Products
# Recyclable and Low Fat Products

## Problem Statement

You are given a table named `Products` with the following structure:

| Column Name | Type    |
|-------------|---------|
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |

- `product_id` is the primary key (a column with unique values) for this table.
- `low_fats` is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
- `recyclable` is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.

Your task is to write a solution to find the IDs of products that are both low fat and recyclable. The result table can be returned in any order.

## Example

### Input
`Products` table:
```
+-------------+----------+------------+
| product_id  | low_fats | recyclable |
+-------------+----------+------------+
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |
+-------------+----------+------------+
```

### Output
```
+-------------+
| product_id  |
+-------------+
| 1           |
| 3           |
+-------------+
```

### Explanation
Only products with IDs 1 and 3 are both low fat and recyclable.

## Solution

```sql
/* Write your PL/SQL query statement below */
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```