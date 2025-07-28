# Problem Statement: Students and Examinations

## Problem Description

Table: `Students`

| Column Name | Type    |
| :---------- | :------ |
| `student_id`| int     |
| `student_name`| varchar |

`student_id` is the primary key (column with unique values) for this table.
Each row of this table contains the ID and the name of one student in the school.

Table: `Subjects`

| Column Name | Type    |
| :---------- | :------ |
| `subject_name`| varchar |

`subject_name` is the primary key (column with unique values) for this table.
Each row of this table contains the name of one subject in the school.

Table: `Examinations`

| Column Name | Type    |
| :---------- | :------ |
| `student_id`| int     |
| `subject_name`| varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.
`student_id` is a foreign key (reference column) to the `Students` table.
`subject_name` is a foreign key (reference column) to the `Subjects` table.
Each row of this table indicates that a student with `student_id` attended the examination of `subject_name`.

Write a solution to find the number of times each student attended each examination.

Return the result table ordered by `student_id` and `subject_name`.

The result format is in the following example.

## Example

**Input:**
Students table:
| student_id | student_name |
| :--------- | :----------- |
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

Subjects table:
| subject_name |
| :----------- |
| Math         |
| Physics      |
| Programming  |

Examinations table:
| student_id | subject_name |
| :--------- | :----------- |
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

**Output:**
| student_id | student_name | subject_name | attended_exams |
| :--------- | :----------- | :----------- | :------------- |
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

**Explanation:**
The table shows the number of times each student attended each examination.
- Student 1 (Alice) attended Math 3 times, Physics 2 times, and Programming 1 time.
- Student 2 (Bob) attended Math 1 time, Physics 0 times, and Programming 1 time.
- Student 6 (Alex) attended Math 0 times, Physics 0 times, and Programming 0 times.
- Student 13 (John) attended Math 1 time, Physics 1 time, and Programming 1 time.
The output is ordered by `student_id` and `subject_name`.

## LeetCode Problem Link

[Students and Examinations - LeetCode](https://leetcode.com/problems/students-and-examinations/)

## Solution
```sql
SELECT s.student_id, s.student_name, sub.subject_name, COUNT(e.student_id) AS attended_exams
FROM Students AS s
CROSS JOIN Subjects AS sub
LEFT JOIN Examinations AS e
ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;
