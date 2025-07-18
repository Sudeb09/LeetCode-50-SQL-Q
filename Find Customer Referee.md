# Problem Statement: Find Customer Referee

## Problem Description

Table: `Customer`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `name`      | varchar |
| `referee_id`| int     |

`id` is the primary key (column with unique values) for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.

Write a solution to report the names of the customer that are **not referred by** the customer with `id = 2`.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Customer table:
| id | name | referee_id |
| :--| :---| :----------|
| 1  | Will | NULL       |
| 2  | Jane | NULL       |
| 3  | Alex | 2          |
| 4  | Bill | NULL       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

**Output:**
| name |
| :---|
| Will |
| Jane |
| Bill |
| Zack |

**Explanation:**
Customers with referee_id 2 are Alex and Mark.
All other customers (Will, Jane, Bill, Zack) are not referred by customer 2.
- Will has `referee_id = NULL`.
- Jane has `referee_id = NULL`.
- Bill has `referee_id = NULL`.
- Zack has `referee_id = 1`.

## LeetCode Problem Link

[Find Customer Referee - LeetCode](https://leetcode.com/problems/find-customer-referee/)

## Solution
```sql
SELECT name
FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL;
