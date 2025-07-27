# Problem Statement: Employee Bonus

## Problem Description

Table: `Employee`

| Column Name | Type    |
| :---------- | :------ |
| `empId`     | int     |
| `name`      | varchar |
| `supervisorId`| int     |
| `salary`    | int     |

`empId` is the primary key (column with unique values) for this table.
Each row of this table indicates the name and the ID of an employee in a company, the ID of their supervisor, and their salary.

Table: `Bonus`

| Column Name | Type    |
| :---------- | :------ |
| `empId`     | int     |
| `bonus`     | int     |

`empId` is the primary key (column with unique values) for this table.
`empId` is a foreign key (reference column) to the `Employee` table.
Each row of this table contains the ID of an employee and their bonus. The bonus is a non-negative integer.

Write a solution to report the name and bonus amount of each employee with a bonus less than `1000`.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Employee table:
| empId | name  | supervisorId | salary |
| :---- | :---- | :----------- | :----- |
| 1     | John  | NULL         | 1000   |
| 2     | Dan   | 1            | 2000   |
| 3     | Brad  | 1            | 4000   |
| 4     | Thomas| 1            | 4000   |

Bonus table:
| empId | bonus |
| :---- | :---- |
| 2     | 500   |
| 4     | 2000  |

**Output:**
| name | bonus |
| :--- | :---- |
| Dan  | 500   |
| John | NULL  |
| Brad | NULL  |

**Explanation:**
- John has no bonus, so `NULL` is considered less than 1000.
- Dan has a bonus of 500, which is less than 1000.
- Brad has no bonus, so `NULL` is considered less than 1000.
- Thomas has a bonus of 2000, which is not less than 1000.

## LeetCode Problem Link

[Employee Bonus - LeetCode](https://leetcode.com/problems/employee-bonus/)

## Solution
```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
