# Problem Statement: Replace Employee ID With The Unique Identifier

## Problem Description

Table: `Employees`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `name`      | varchar |

`id` is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.

Table: `EmployeeUNI`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `unique_id` | int     |

(`id`, `unique_id`) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Employees table:
| id | name  |
| :--| :---- |
| 1  | Alice |
| 7  | Bob   |
| 11 | Meir  |
| 90 | Winston |
| 3  | Grant |

EmployeeUNI table:
| id | unique_id |
| :--| :-------- |
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

**Output:**
| unique_id | name    |
| :-------- | :------ |
| NULL      | Alice   |
| NULL      | Bob     |
| 2         | Meir    |
| 3         | Winston |
| 1         | Grant   |

**Explanation:**
- Alice and Bob do not have a unique ID, so we show `null` for them.
- Meir has unique ID 2.
- Winston has unique ID 3.
- Grant has unique ID 1.

## LeetCode Problem Link

[Replace Employee ID With The Unique Identifier - LeetCode](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

## Solution
```sql
SELECT eu.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
ON e.id = eu.id;
