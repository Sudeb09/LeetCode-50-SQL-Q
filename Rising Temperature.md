# Problem Statement: Rising Temperature

## Problem Description

Table: `Weather`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `recordDate`| date    |
| `temperature`| int     |

`id` is the primary key (column with unique values) for this table.
This table contains information about the temperature on a certain day.

Write a solution to find all dates' `id`s with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Weather table:
| id | recordDate | temperature |
| :--| :--------- | :---------- |
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |

**Output:**
| id |
| :--|
| 2  |
| 4  |

**Explanation:**
- On 2015-01-02, the temperature was 25. This was higher than the temperature of 10 on 2015-01-01.
- On 2015-01-03, the temperature was 20. This was not higher than the temperature of 25 on 2015-01-02.
- On 2015-01-04, the temperature was 30. This was higher than the temperature of 20 on 2015-01-03.

## LeetCode Problem Link

[Rising Temperature - LeetCode](https://leetcode.com/problems/rising-temperature/)

## Solution
```sql
SELECT w1.id
FROM Weather w1, Weather w2
WHERE DATEDIFF(w1.recordDate, w2.recordDate) = 1
AND w1.temperature > w2.temperature;
