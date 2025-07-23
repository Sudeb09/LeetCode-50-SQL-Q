# Problem Statement: Product Sales Analysis I

## Problem Description

Table: `Sales`

| Column Name | Type    |
| :---------- | :------ |
| `sale_id`   | int     |
| `product_id`| int     |
| `year`      | int     |
| `quantity`  | int     |
| `price`     | int     |

(`sale_id`, `year`) is the primary key (combination of columns with unique values) of this table.
`product_id` is a foreign key (reference column) to the `Product` table.
Each row of this table shows a sale on the product `product_id` in a certain `year`.
and `quantity` is the amount of `price` of this sale.

Table: `Product`

| Column Name  | Type    |
| :----------- | :------ |
| `product_id` | int     |
| `product_name`| varchar |

`product_id` is the primary key (column with unique values) of this table.
Each row of this table indicates the `product_id` and `product_name` of a product.

Write a solution to report the `product_name`, `year`, and `price` for each sale_id in the `Sales` table.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Sales table:
| sale_id | product_id | year | quantity | price   |
| :------ | :--------- | :--- | :------- | :----   |
| 1       | 100        | 2008 | 10       | 5000    |
| 2       | 100        | 2009 | 12       | 5000    |
| 7       | 200        | 2011 | 15       | 9000    |

Product table:
| product_id | product_name |
| :--------- | :----------- |
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

**Output:**
| product_name | year | price   |
| :----------- | :--- | :----   |
| Nokia        | 2008 | 5000    |
| Nokia        | 2009 | 5000    |
| Apple        | 2011 | 9000    |

**Explanation:**
- The first sale has `product_id` 100, which is "Nokia". The sale was in 2008 with a price of 5000.
- The second sale has `product_id` 100, which is "Nokia". The sale was in 2009 with a price of 5000.
- The third sale has `product_id` 200, which is "Apple". The sale was in 2011 with a price of 9000.

## LeetCode Problem Link

[Product Sales Analysis I - LeetCode](https://leetcode.com/problems/product-sales-analysis-i/)

## Solution
```sql
SELECT p.product_name, s.year, s.price
FROM Sales AS s
JOIN Product AS p
ON s.product_id = p.product_id;
