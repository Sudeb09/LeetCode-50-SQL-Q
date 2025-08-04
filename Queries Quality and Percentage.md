# Problem Statement: Queries Quality and Percentage

## Problem Description

Table: `Queries`

| Column Name | Type    |
| :---------- | :------ |
| `query_name`| varchar |
| `result`    | varchar |
| `position`  | int     |
| `rating`    | int     |

There is no primary key (column with unique values) for this table, and it may have duplicate rows.
This table contains information about the queries and their results.
`query_name` is the name of a query.
`result` is the result of the query at `position`.
`position` is the result position.
`rating` is the rating of the result, from 1 (bad) to 5 (excellent).

The **query quality** is the average of the ratio between the `rating` and its `position` for all results for a specific `query_name`.
The **poor query percentage** is the percentage of all queries with a `rating` less than 3.

Write a solution to find the `query_name`, `quality`, and `poor_query_percentage`.

Both `quality` and `poor_query_percentage` should be rounded to 2 decimal places.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Queries table:
| query_name | result            | position | rating |
| :--------- | :---------------- | :------- | :----- |
| Dog        | Golden Retriever  | 1        | 5      |
| Dog        | German Shepherd   | 2        | 5      |
| Dog        | Mule              | 200      | 1      |
| Cat        | Shirazi           | 5        | 2      |
| Cat        | Siamese           | 3        | 3      |
| Cat        | Sphynx            | 7        | 4      |

**Output:**
| query_name | quality | poor_query_percentage |
| :--------- | :------ | :-------------------- |
| Dog        | 2.50    | 33.33                 |
| Cat        | 0.66    | 33.33                 |

**Explanation:**
For query "Dog":
- Quality: ((5 / 1) + (5 / 2) + (1 / 200)) / 3 = (5 + 2.5 + 0.005) / 3 = 7.505 / 3 = 2.5016...
  Rounded to 2 decimal places: 2.50.
- Poor query percentage: (Number of ratings < 3) / (Total number of ratings) * 100 = (1 / 3) * 100 = 33.333...%
  Rounded to 2 decimal places: 33.33.

For query "Cat":
- Quality: ((2 / 5) + (3 / 3) + (4 / 7)) / 3 = (0.4 + 1 + 0.5714...) / 3 = 1.9714... / 3 = 0.6571...
  Rounded to 2 decimal places: 0.66.
- Poor query percentage: (Number of ratings < 3) / (Total number of ratings) * 100 = (1 / 3) * 100 = 33.333...%
  Rounded to 2 decimal places: 33.33.

## LeetCode Problem Link

[Queries Quality and Percentage - LeetCode](https://leetcode.com/problems/queries-quality-and-percentage/)

## Solution
```sql
SELECT
    query_name,
    ROUND(AVG(rating / position), 2) AS quality,
    ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS poor_query_percentage
FROM
    Queries
WHERE
    query_name IS NOT NULL
GROUP BY
    query_name;
