# Problem Statement: Invalid Tweets

## Problem Description

Table: `Tweets`

| Column Name | Type    |
| :---------- | :------ |
| `tweet_id`  | int     |
| `content`   | varchar |

`tweet_id` is the primary key (column with unique values) for this table.
This table contains all tweets in a social media app.

Write a solution to find the IDs of the invalid tweets.
A tweet is invalid if its number of characters is strictly greater than 15.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Tweets table:
| tweet_id | content                          |
| :--------- | :------------------------------- |
| 1          | Vote for Biden                   |
| 2          | Let us make America great again! |

**Output:**
| tweet_id |
| :--------- |
| 2          |

**Explanation:**
- Tweet 1 has a length of 14. It is a valid tweet.
- Tweet 2 has a length of 32. It is an invalid tweet.

## LeetCode Problem Link

[Invalid Tweets - LeetCode](https://leetcode.com/problems/invalid-tweets/)

## Solution
```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
