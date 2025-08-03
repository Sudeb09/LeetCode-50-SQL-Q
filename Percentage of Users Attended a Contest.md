# Problem Statement: Percentage of Users Attended a Contest

## Problem Description

Table: `Users`

| Column Name | Type    |
| :---------- | :------ |
| `user_id`   | int     |
| `user_name` | varchar |

`user_id` is the primary key (column with unique values) for this table.
Each row of this table contains the name and the ID of a user.

Table: `Register`

| Column Name | Type    |
| :---------- | :------ |
| `contest_id`| int     |
| `user_id`   | int     |

(`contest_id`, `user_id`) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the ID of a user and the contest they registered into.

Write a solution to find the percentage of the users registered in each contest rounded to two decimals.

Return the result table ordered by `percentage` in **descending** order. In case of a tie, order it by `contest_id` in **ascending** order.

The result format is in the following example.

## Example

**Input:**
Users table:
| user_id | user_name |
| :------ | :-------- |
| 6       | Alice     |
| 2       | Bob       |
| 7       | Alex      |

Register table:
| contest_id | user_id |
| :--------- | :------ |
| 215        | 6       |
| 209        | 2       |
| 208        | 2       |
| 210        | 6       |
| 208        | 6       |
| 209        | 7       |
| 209        | 6       |
| 215        | 7       |
| 208        | 7       |
| 210        | 2       |
| 207        | 2       |
| 210        | 7       |

**Output:**
| contest_id | percentage |
| :--------- | :--------- |
| 208        | 100.00     |
| 209        | 100.00     |
| 210        | 100.00     |
| 215        | 66.67      |
| 207        | 33.33      |

**Explanation:**
Total number of users is 3 (Alice, Bob, Alex).

- **Contest 208:** Users (2, 6, 7) registered. All 3 users registered. Percentage = (3/3) * 100 = 100.00%
- **Contest 209:** Users (2, 6, 7) registered. All 3 users registered. Percentage = (3/3) * 100 = 100.00%
- **Contest 210:** Users (2, 6, 7) registered. All 3 users registered. Percentage = (3/3) * 100 = 100.00%
- **Contest 215:** Users (6, 7) registered. 2 out of 3 users registered. Percentage = (2/3) * 100 = 66.666...% rounded to 66.67%
- **Contest 207:** User (2) registered. 1 out of 3 users registered. Percentage = (1/3) * 100 = 33.333...% rounded to 33.33%

The output is ordered by percentage in descending order, and then by contest_id in ascending order for ties.

## LeetCode Problem Link

[Percentage of Users Attended in a Contest - LeetCode](https://leetcode.com/problems/percentage-of-users-attended-in-a-contest/)

## Solution
```sql
SELECT r.contest_id,
       ROUND(COUNT(DISTINCT r.user_id) * 100.0 / (SELECT COUNT(user_id) FROM Users), 2) AS percentage
FROM Register AS r
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;
