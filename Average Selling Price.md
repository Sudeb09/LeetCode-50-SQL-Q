# Problem Statement: Average Selling Price

## Problem Description

Table: `Prices`

| Column Name | Type    |
| :---------- | :------ |
| `product_id`| int     |
| `start_date`| date    |
| `end_date`  | date    |
| `price`     | int     |

(`product_id`, `start_date`, `end_date`) is the primary key (combination of columns with unique values) for this table.
Each row of this table indicates the price of a product during a specific period.
Note that the price is the same for all products with the same `product_id`.

Table: `UnitsSold`

| Column Name | Type    |
| :---------- | :------ |
| `product_id`| int     |
| `purchase_date`| date    |
| `units`     | int     |

There is no primary key (column with unique values) for this table. It can have duplicate rows.
`product_id` is a foreign key (reference column) to the `Prices` table.
Each row of this table indicates the date, `product_id`, and `units` sold.

Write a solution to find the average selling price for each product. `average_price` should be rounded to 2 decimal places.

Return the result table in any order.

The result format is in the following example.

## Example

**Input:**
Prices table:
| product_id | start_date | end_date   | price |
| :--------- | :--------- | :--------- | :---- |
| 1          | 2019-02-17 | 2019-02-28 | 5     |
| 1          | 2019-03-01 | 2019-03-22 | 20    |
| 2          | 2019-02-01 | 2019-02-20 | 15    |
| 2          | 2019-02-21 | 2019-03-31 | 30    |

UnitsSold table:
| product_id | purchase_date | units |
| :--------- | :------------ | :---- |
| 1          | 2019-02-25    | 100   |
| 1          | 2019-03-01    | 15    |
| 2          | 2019-02-10    | 200   |
| 2          | 2019-03-22    | 30    |

**Output:**
| product_id | average_price |
| :--------- | :------------ |
| 1          | 6.96          |
| 2          | 16.96         |

**Explanation:**
For product 1:
- From 2019-02-17 to 2019-02-28, price is 5.
- From 2019-03-01 to 2019-03-22, price is 20.
- The product was sold on 2019-02-25 for 100 units. Its price was 5.
- The product was sold on 2019-03-01 for 15 units. Its price was 20.
Average price = ((100 * 5) + (15 * 20)) / (100 + 15) = (500 + 300) / 115 = 800 / 115 = 6.95652...
Rounded to 2 decimal places: 6.96

For product 2:
- From 2019-02-01 to 2019-02-20, price is 15.
- From 2019-02-21 to 2019-03-31, price is 30.
- The product was sold on 2019-02-10 for 200 units. Its price was 15.
- The product was sold on 2019-03-22 for 30 units. Its price was 30.
Average price = ((200 * 15) + (30 * 30)) / (200 + 30) = (3000 + 900) / 230 = 3900 / 230 = 16.95652...
Rounded to 2 decimal places: 16.96

## LeetCode Problem Link

[Average Selling Price - LeetCode](https://leetcode.com/problems/average-selling-price/)

## Solution
```sql
SELECT 
    p.product_id,
    ROUND(
        COALESCE(SUM(u.units * p.price) * 1.0 / NULLIF(SUM(u.units), 0), 0),
        2
    ) AS average_price
FROM 
    Prices p
LEFT JOIN 
    UnitsSold u
    ON p.product_id = u.product_id 
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY 
    p.product_id;
