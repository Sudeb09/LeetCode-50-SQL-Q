# Problem Statement: Article Views I

## Problem Description

Table: `Views`

| Column Name | Type    |
| :---------- | :------ |
| `article_id`| int     |
| `author_id` | int     |
| `viewer_id` | int     |
| `view_date` | date    |

There is no primary key (column with unique values) for this table, and it may have duplicate rows.
Each row of this table indicates that some `viewer_id` viewed an article written by `author_id` on `view_date`.
Note that author_id and viewer_id are equal in some cases, meaning the author of an article might also be a viewer of the same article.

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by `id` in ascending order.

The result format is in the following example.

## Example

**Input:**
Views table:
| article_id | author_id | viewer_id | view_date  |
| :--------- | :-------- | :-------- | :--------- |
| 1          | 3         | 5         | 2019-01-01 |
| 1          | 3         | 6         | 2019-01-02 |
| 2          | 7         | 7         | 2019-01-01 |
| 2          | 7         | 6         | 2019-01-02 |
| 4          | 7         | 1         | 2019-01-02 |
| 3          | 4         | 4         | 2019-01-02 |
| 3          | 4         | 4         | 2019-01-02 |

**Output:**
| id |
| :--|
| 4  |
| 7  |

**Explanation:**
- `author_id` 7 viewed their own article (article_id 2).
- `author_id` 4 viewed their own article (article_id 3).
- `author_id` 3 did not view any of their own articles.
Note that the output should be sorted in ascending order.

## LeetCode Problem Link

[Article Views I - LeetCode](https://leetcode.com/problems/article-views-i/)

## Solution
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
