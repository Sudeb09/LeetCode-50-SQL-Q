# Problem Statement: Recycleable and Low Fat Products

## Problem Description

Table: `Products`

| Column Name | Type    |
| :---------- | :------ |
| `product_id`  | int     |
| `low_fats`    | enum    |
| `recyclable`  | enum    |

`product_id` is the primary key (column with unique values) for this table.
`low_fats` is an ENUM (`'Y'`, `'N'`) of type string.
`recyclable` is an ENUM (`'Y'`, `'N'`) of type string.

Write a solution to find the `product_id` of the products that are both low fat and recyclable.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Products table:
| product_id | low_fats | recyclable |
| :--------- | :------- | :--------- |
| 0          | Y        | N          |
| 1          | Y        | Y          |
| 2          | N        | Y          |
| 3          | Y        | Y          |
| 4          | N        | N          |

**Output:**
| product_id |
| :--------- |
| 1          |
| 3          |

**Explanation:**
- Product 0 is low fat but not recyclable.
- Product 1 is both low fat and recyclable.
- Product 2 is recyclable but not low fat.
- Product 3 is both low fat and recyclable.
- Product 4 is neither low fat nor recyclable.
Only products 1 and 3 are both low fat and recyclable.

## LeetCode Problem Link

[Recyclable and Low Fat Products - LeetCode](https://leetcode.com/problems/recyclable-and-low-fat-products/)

## Solution
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
