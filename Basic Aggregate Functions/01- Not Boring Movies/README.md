# 01- Not Boring Movies

## Problem Description

You are given a table `Cinema` with the following structure:

```
+----------------+----------+
| Column Name    | Type     |
+----------------+----------+
| id             | int      |
| movie          | varchar  |
| description    | varchar  |
| rating         | float    |
+----------------+----------+
```

- `id` is the primary key (column with unique values) for this table.
- Each row contains information about the name of a movie, its genre, and its rating.
- `rating` is a 2 decimal places float in the range [0, 10]

Write a solution to report the movies with an odd-numbered ID and a description that is not `"boring"`.
Return the result table ordered by `rating` **in descending order**.

### Example 1:

**Input:** 
Cinema table:
```
+----+------------+-------------+--------+
| id | movie      | description | rating |
+----+------------+-------------+--------+
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | Fantacy     | 8.6    |
| 5  | House card | Interesting | 9.1    |
+----+------------+-------------+--------+
```

**Output:** 
```
+----+------------+-------------+--------+
| id | movie      | description | rating |
+----+------------+-------------+--------+
| 5  | House card | Interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |
+----+------------+-------------+--------+
```

**Explanation:** 
We have three movies with odd-numbered IDs: 1, 3, and 5. The movie with ID = 3 is boring so we do not include it in the answer.

## Solution

```sql
SELECT *
FROM Cinema c
WHERE MOD(id,2) != 0 AND NOT description = 'boring'
ORDER BY rating DESC
```

This SQL query selects all columns from the Cinema table where the ID is odd (using the MOD function) and the description is not 'boring'. The results are then ordered by the rating in descending order.