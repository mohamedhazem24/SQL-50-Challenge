# 04- Article Views I
## Problem Description

Given a table `Views`, the task is to find all the authors that viewed at least one of their own articles.

### Table Schema

**Views**

| Column Name | Type    |
|-------------|---------|
| article_id  | int     |
| author_id   | int     |
| viewer_id   | int     |
| view_date   | date    |

- There is no primary key for this table, and it may contain duplicate rows.
- Each row indicates that some viewer viewed an article (written by some author) on some date.
- Note that equal `author_id` and `viewer_id` indicate the same person.

### Requirements

Return the authors that viewed at least one of their own articles, sorted by `id` in ascending order.

### Example

#### Input:

**Views table:**

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

#### Output:

| id   |
|------|
| 4    |
| 7    |

## Solution

```sql
/* Write your PL/SQL query statement below */
SELECT DISTINCT author_id AS id
FROM Views 
WHERE author_id = viewer_id 
ORDER BY author_id;
```