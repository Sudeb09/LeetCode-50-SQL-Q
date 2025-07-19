# Problem Statement: Big Countries

## Problem Description

Table: `World`

| Column Name | Type    |
| :---------- | :------ |
| `name`      | varchar |
| `continent` | varchar |
| `area`      | int     |
| `population`| int     |
| `gdp`       | bigint  |

`name` is the primary key (column with unique values) for this table.
Each row of this table gives information about the name of a country, the continent to which it belongs, its area, the population, and its GDP value.

A country is said to be a **big country** if it has an area of at least three million (i.e., `3,000,000 km^2`) or a population of at least twenty-five million (i.e., `25,000,000`).

Write a solution to find the name, population, and area of the big countries.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
World table:
| name        | continent | area    | population | gdp          |
| :---------- | :-------- | :------ | :--------- | :----------- |
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 13402000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78169      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

**Output:**
| name        | population | area    |
| :---------- | :--------- | :------ |
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |

**Explanation:**
- Afghanistan has a population of 25,500,100, which is >= 25,000,000.
- Albania has an area of 28,748 and a population of 2,831,741, neither of which meet the criteria.
- Algeria has an area of 2,381,741 and a population of 37,100,000. Its population is >= 25,000,000.
- Andorra has an area of 468 and a population of 78,169, neither of which meet the criteria.
- Angola has an area of 1,246,700 and a population of 20,609,294, neither of which meet the criteria.
Therefore, Afghanistan and Algeria are big countries.

## LeetCode Problem Link

[Big Countries - LeetCode](https://leetcode.com/problems/big-countries/)

## Solution
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
