# Problem Statement: Project Employees I

## Problem Description

Table: `Project`

| Column Name | Type    |
| :---------- | :------ |
| `project_id`| int     |
| `employee_id`| int     |

(`project_id`, `employee_id`) is the primary key (combination of columns with unique values) of this table.
`employee_id` is a foreign key (reference column) to the `Employee` table.
Each row of this table indicates that the employee with `employee_id` is working on the project with `project_id`.

Table: `Employee`

| Column Name | Type    |
| :---------- | :------ |
| `employee_id`| int     |
| `name`      | varchar |
| `experience_years`| int     |

`employee_id` is the primary key (column with unique values) of this table.
Each row of this table contains the `id`, `name`, and the `experience_years` of an employee.

Write a solution to report the average `experience_years` of all the employees for each project.

Return the result table in any order, rounded to 2 decimal places.

The result format is in the following example.

## Example

**Input:**
Project table:
| project_id | employee_id |
| :--------- | :---------- |
| 1          | 1           |
| 1          | 2           |
| 1          | 3           |
| 2          | 1           |
| 2          | 4           |

Employee table:
| employee_id | name  | experience_years |
| :---------- | :---- | :--------------- |
| 1           | Khadija | 3                |
| 2           | Darun | 1                |
| 3           | Aseel | 2                |
| 4           | Khaled| 2                |

**Output:**
| project_id | average_years |
| :--------- | :------------ |
| 1          | 2.00          |
| 2          | 2.50          |

**Explanation:**
For project 1: employees 1, 2, and 3 are working on it. Their average experience years is (3 + 1 + 2) / 3 = 2.00.
For project 2: employees 1 and 4 are working on it. Their average experience years is (3 + 2) / 2 = 2.50.

## LeetCode Problem Link

[Project Employees I - LeetCode](https://leetcode.com/problems/project-employees-i/)

## Solution
```sql
SELECT p.project_id, ROUND(AVG(e.experience_years), 2) AS average_years
FROM Project AS p
JOIN Employee AS e
ON p.employee_id = e.employee_id
GROUP BY p.project_id;
