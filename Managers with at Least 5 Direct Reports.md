# Problem Statement: Managers with at Least 5 Direct Reports

## Problem Description

Table: `Employee`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `name`      | varchar |
| `department`| varchar |
| `managerId` | int     |

`id` is the primary key (column with unique values) for this table.
Each row of this table indicates the `id`, `name`, and `department` of an employee. It also contains the `id` of their `manager`. If `managerId` is `NULL`, then the employee does not have a manager (i.e., they are the CEO).

Write a solution to find the names of managers who have at least **five direct reports**.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Employee table:
| id | name  | department | managerId |
| :--| :---- | :--------- | :-------- |
| 101| John  | A          | NULL      |
| 102| Dan   | A          | 101       |
| 103| James | A          | 101       |
| 104| Amy   | A          | 101       |
| 105| Anne  | A          | 101       |
| 106| Ron   | B          | 101       |

**Output:**
| name |
| :--- |
| John |

**Explanation:**
- John (id 101) is the manager of Dan, James, Amy, Anne, and Ron.
- All five employees (102, 103, 104, 105, and 106) report directly to John.
- Since John has 5 direct reports, we include his name in the output.

## LeetCode Problem Link

[Managers with at Least 5 Direct Reports - LeetCode](https://leetcode.com/problems/managers-with-at-least-five-direct-reports/)

## Solution
```sql
SELECT e1.name
FROM Employee AS e1
JOIN Employee AS e2
ON e1.id = e2.managerId
GROUP BY e1.id, e1.name
HAVING COUNT(e2.id) >= 5;
