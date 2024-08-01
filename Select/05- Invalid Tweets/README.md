# 05- Invalid Tweets
## Problem Description

Given a table `Tweets`, the task is to find the IDs of the invalid tweets. A tweet is considered invalid if the number of characters in the content of the tweet is strictly greater than 15.

### Table Schema

**Tweets**

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |

- `tweet_id` is the primary key for this table.
- This table contains all the tweets in a social media app.

### Requirements

Return the IDs of the tweets that are invalid, where the content length is strictly greater than 15 characters. The result can be returned in any order.

### Example

#### Input:

**Tweets table:**

| tweet_id | content                          |
|----------|----------------------------------|
| 1        | Vote for Biden                    |
| 2        | Let us make America great again!  |

#### Output:

| tweet_id |
|----------|
| 2        |

**Explanation:** 
- Tweet 1 has a length of 14 characters, so it is a valid tweet.
- Tweet 2 has a length of 32 characters, so it is an invalid tweet.

## Solution

```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```