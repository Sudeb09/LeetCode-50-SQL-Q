# Problem Statement: Average Time of Process Per Machine

## Problem Description

Table: `Activity`

| Column Name | Type    |
| :---------- | :------ |
| `machine_id`| int     |
| `process_id`| int     |
| `activity_type`| enum    |
| `timestamp` | float   |

The table shows the user activities for a factory.
(`machine_id`, `process_id`, `activity_type`) is the primary key (combination of columns with unique values) of this table.
`machine_id` is the ID of a machine.
`process_id` is the ID of a process running on the machine with a given `machine_id`.
`activity_type` is an ENUM (`'start'`, `'end'`) indicating whether an activity is a start or end activity.
`timestamp` is a float representing the current time in seconds.

Each `process_id` on a specific `machine_id` has **exactly two** activities: a `'start'` activity and an `'end'` activity.

For each machine, find the average time each process takes to complete.

The time to complete a process is the `'end'` timestamp minus the `'start'` timestamp.
Average time is calculated by the total time to complete all processes by the number of processes.

Return the result table in any order, rounded to 3 decimal places.

The result format is in the following example.

## Example

**Input:**
Activity table:
| machine_id | process_id | activity_type | timestamp |
| :--------- | :--------- | :------------ | :-------- |
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.500     |

**Output:**
| machine_id | processing_time |
| :--------- | :-------------- |
| 0          | 0.888           |
| 1          | 0.995           |
| 2          | 0.400           |

**Explanation:**
For machine 0:
- Process 0: `timestamp` of end activity - `timestamp` of start activity = 1.520 - 0.712 = 0.808
- Process 1: `timestamp` of end activity - `timestamp` of start activity = 4.120 - 3.140 = 0.980
Average processing time for machine 0 = (0.808 + 0.980) / 2 = 0.894

For machine 1:
- Process 0: `timestamp` of end activity - `timestamp` of start activity = 1.550 - 0.550 = 1.000
- Process 1: `timestamp` of end activity - `timestamp` of start activity = 1.420 - 0.430 = 0.990
Average processing time for machine 1 = (1.000 + 0.990) / 2 = 0.995

For machine 2:
- Process 0: `timestamp` of end activity - `timestamp` of start activity = 4.500 - 4.100 = 0.400
Average processing time for machine 2 = 0.400 / 1 = 0.400

## LeetCode Problem Link

[Average Time of Process Per Machine - LeetCode](https://leetcode.com/problems/average-time-of-process-per-machine/)

## Solution
```sql
SELECT a1.machine_id, ROUND(AVG(a2.timestamp - a1.timestamp), 3) AS processing_time
FROM Activity a1
JOIN Activity a2
ON a1.machine_id = a2.machine_id
AND a1.process_id = a2.process_id
WHERE a1.activity_type = 'start' AND a2.activity_type = 'end'
GROUP BY a1.machine_id;
