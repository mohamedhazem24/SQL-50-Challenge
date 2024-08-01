# 03- Movie Rating

---

### Tables

**Movies**

| Column Name | Type    |
|-------------|---------|
| movie_id    | int     |
| title       | varchar |

**Users**

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| name        | varchar |

**MovieRating**

| Column Name | Type    |
|-------------|---------|
| movie_id    | int     |
| user_id     | int     |
| rating      | int     |
| created_at  | date    |

### Problem Statement

1. Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.
2. Find the movie name with the highest average rating in February 2020. In case of a tie, return the lexicographically smaller movie name.

### Example

**Input:**

**Movies Table:**

| movie_id | title    |
|----------|----------|
| 1        | Avengers |
| 2        | Frozen 2 |
| 3        | Joker    |

**Users Table:**

| user_id | name  |
|---------|-------|
| 1       | Daniel|
| 2       | Monica|
| 3       | Maria |
| 4       | James |

**MovieRating Table:**

| movie_id | user_id | rating | created_at |
|----------|---------|--------|------------|
| 1        | 1       | 3      | 2020-01-12 |
| 1        | 2       | 4      | 2020-02-11 |
| 1        | 3       | 2      | 2020-02-12 |
| 1        | 4       | 1      | 2020-01-01 |
| 2        | 1       | 5      | 2020-02-17 |
| 2        | 2       | 2      | 2020-02-01 |
| 2        | 3       | 2      | 2020-03-01 |
| 3        | 1       | 3      | 2020-02-22 |
| 3        | 2       | 4      | 2020-02-25 |

**Output:**

| results    |
|------------|
| Daniel     |
| Frozen 2   |

**Explanation:**
- Daniel and Monica have each rated 3 movies ("Avengers", "Frozen 2", "Joker"), but Daniel's name is lexicographically smaller.
- "Frozen 2" and "Joker" have the highest average rating of 3.5 in February 2020, but "Frozen 2" is lexicographically smaller.

### Solution

```sql
SELECT results
FROM (
    SELECT u.name AS results, COUNT(mr.rating) AS movie_count
    FROM MovieRating mr
    LEFT JOIN Users u ON mr.user_id = u.user_id
    GROUP BY u.name
    ORDER BY movie_count DESC, u.name ASC
)
WHERE ROWNUM = 1
UNION ALL
SELECT results
FROM (
    SELECT m.title AS results, AVG(mr.rating) AS movie_avg
    FROM MovieRating mr
    LEFT JOIN Movies m ON mr.movie_id = m.movie_id
    WHERE mr.created_at BETWEEN TO_DATE('2020-02-01', 'YYYY-MM-DD') AND TO_DATE('2020-02-29', 'YYYY-MM-DD')
    GROUP BY m.title
    ORDER BY movie_avg DESC, m.title ASC
)
WHERE ROWNUM = 1;
```

---

