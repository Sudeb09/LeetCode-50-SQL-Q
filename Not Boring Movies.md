# Problem Statement: Not Boring Movies

## Problem Description

Table: `Cinema`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `movie`     | varchar |
| `description`| varchar |
| `rating`    | float   |

`id` is the primary key (column with unique values) for this table.
Each row of this table indicates a movie's `id`, `title`, `description`, and its `rating`.

Write a solution to report the movies with an odd `id` and a description that is **not** `'boring'`.

Return the result table ordered by `rating` in **descending** order.

The result format is in the following example.

## Example

**Input:**
Cinema table:
| id | movie      | description | rating |
| :--| :--------- | :---------- | :----- |
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | fantasy     | 8.6    |
| 5  | House card | interesting | 9.1    |

**Output:**
| id | movie      | description | rating |
| :--| :--------- | :---------- | :----- |
| 5  | House card | interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |

**Explanation:**
- `id` 1 is odd and its description is not 'boring'.
- `id` 2 is even.
- `id` 3 is odd but its description is 'boring'.
- `id` 4 is even.
- `id` 5 is odd and its description is not 'boring'.
The movies are ordered by rating in descending order.

## LeetCode Problem Link

[Not Boring Movies - LeetCode](https://leetcode.com/problems/not-boring-movies/)

## Solution
```sql
SELECT *
FROM Cinema
WHERE id % 2 != 0 AND description != 'boring'
ORDER BY rating DESC;
