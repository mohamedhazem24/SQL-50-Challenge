# 06- Last Person to Fit in the Bus


---

### Table: Queue

| Column Name | Type    |
|-------------|---------|
| person_id   | int     |
| person_name | varchar |
| weight      | int     |
| turn        | int     |

**Primary Key:** person_id  
**Description:**  
- `person_id` contains unique values for each person.
- `person_name` is the name of the person.
- `weight` is the weight of the person in kilograms.
- `turn` determines the order of boarding the bus, where `turn=1` denotes the first person to board and `turn=n` denotes the last person to board.

### Problem Statement

There is a queue of people waiting to board a bus. The bus has a weight limit of 1000 kilograms, so some people may not be able to board. Find the `person_name` of the last person that can fit on the bus without exceeding the weight limit. The test cases are generated such that the first person does not exceed the weight limit.

### Example

**Input:**

| person_id | person_name | weight | turn |
|-----------|-------------|--------|------|
| 5         | Alice       | 250    | 1    |
| 4         | Bob         | 175    | 5    |
| 3         | Alex        | 350    | 2    |
| 6         | John Cena   | 400    | 3    |
| 1         | Winston     | 500    | 6    |
| 2         | Marie       | 200    | 4    |

**Output:**

| person_name |
|-------------|
| John Cena   |

**Explanation:**

The following table is ordered by `turn` for simplicity:

| Turn | ID | Name      | Weight | Total Weight |
|------|----|-----------|--------|--------------|
| 1    | 5  | Alice     | 250    | 250          |
| 2    | 3  | Alex      | 350    | 600          |
| 3    | 6  | John Cena | 400    | 1000         | (last person to board)
| 4    | 2  | Marie     | 200    | 1200         | (cannot board)
| 5    | 4  | Bob       | 175    | ___          |
| 6    | 1  | Winston   | 500    | ___          |

### Solution

```sql
SELECT person_name 
FROM Queue
WHERE turn = (
    SELECT MAX(turn)
    FROM (
        SELECT person_id, person_name, weight, turn,
               SUM(weight) OVER (ORDER BY turn ROWS UNBOUNDED PRECEDING) AS cum_W
        FROM Queue
    )
    WHERE cum_W <= 1000
);
```


