# Problem Statement: Monthly Transactions I

## Problem Description

Table: `Transactions`

| Column Name | Type    |
| :---------- | :------ |
| `id`        | int     |
| `country`   | varchar |
| `state`     | enum    |
| `amount`    | int     |
| `trans_date`| date    |

`id` is the primary key (column with unique values) for this table.
The `state` column is an ENUM of type (`'approved'`, `'declined'`).
This table contains information about transactions, including their ID, country, state, amount, and date.

Write a solution to find for each month and country: the total number of transactions, the number of approved transactions, the total amount of all transactions, and the total amount of approved transactions.

Return the result table in any order.

The result format is in the following example.

-----

## Example

**Input:**
Transactions table:
| id | country | state    | amount | trans\_date |
| :--| :------ | :------- | :----- | :--------- |
| 121| US      | approved | 1000   | 2018-12-18 |
| 122| US      | declined | 2000   | 2018-12-19 |
| 123| US      | approved | 2000   | 2019-01-01 |
| 124| DE      | approved | 2000   | 2019-01-07 |

**Output:**
| month   | country | trans\_count | approved\_count | trans\_total\_amount | approved\_total\_amount |
| :------ | :------ | :---------- | :------------- | :----------------- | :-------------------- |
| 2018-12 | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01 | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01 | DE      | 1           | 1              | 2000               | 2000                  |

**Explanation:**

  - **In 2018-12 for US:**
      - There were 2 transactions (IDs 121 and 122).
      - 1 of these was approved.
      - The total amount was 1000 + 2000 = 3000.
      - The total approved amount was 1000.
  - **In 2019-01 for US:**
      - There was 1 transaction (ID 123).
      - 1 of these was approved.
      - The total amount was 2000.
      - The total approved amount was 2000.
  - **In 2019-01 for DE:**
      - There was 1 transaction (ID 124).
      - 1 of these was approved.
      - The total amount was 2000.
      - The total approved amount was 2000.

-----

## LeetCode Problem Link

[Monthly Transactions I - LeetCode](https://leetcode.com/problems/monthly-transactions-i/)

-----

## Solution

```sql
SELECT
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(id) AS trans_count,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM
    Transactions
GROUP BY
    month,
    country;
```
