### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (GROUP BY) (1327. List the Products Ordered in a Period)
- *table* : Products, Orders

<br>

**Products**
|column|type|
|---|---|
| product_id       | int     |
| product_name     | varchar |
| product_category | varchar |

product_id is the primary key (column with unique values) for this table.
This table contains data about the company's products.

<br>

**Orders**
|column|type|
|---|---|
| product_id    | int     |
| order_date    | date    |
| unit          | int     |

This table may have duplicate rows.
product_id is a foreign key (reference column) to the Products table.
unit is the number of products ordered in order_date.

<br>

### Problem
Write a solution to get the names of products that have at least 100 units ordered in February 2020 and their amount.

Return the result table in any order.

<br>

**Sample Input**

*Products*
| product_id  | product_name          | product_category |
|---|---|---|
| 1           | Leetcode Solutions    | Book             |
| 2           | Jewels of Stringology | Book             |
| 3           | HP                    | Laptop           |
| 4           | Lenovo                | Laptop           |
| 5           | Leetcode Kit          | T-shirt          |

<br>

*Orders*
| product_id   | order_date   | unit     |
|---|---|---|
| 1            | 2020-02-05   | 60       |
| 1            | 2020-02-10   | 70       |
| 2            | 2020-01-18   | 30       |
| 2            | 2020-02-11   | 80       |
| 3            | 2020-02-17   | 2        |
| 3            | 2020-02-24   | 3        |
| 4            | 2020-03-01   | 20       |
| 4            | 2020-03-04   | 30       |
| 4            | 2020-03-04   | 60       |
| 5            | 2020-02-25   | 50       |
| 5            | 2020-02-27   | 50       |
| 5            | 2020-03-01   | 50       |

<br>

**Sample Output**

| product_name       | unit    |
|---|---|
| Leetcode Solutions | 130     |
| Leetcode Kit       | 100     |

<br>

### Solving

```sql
SELECT P.product_name, SUM(O.unit) AS unit
FROM Orders O
 LEFT JOIN Products P USING (product_id)
WHERE DATE_FORMAT(O.order_date, '%Y-%m') = '2020-02'
GROUP BY O.product_id
HAVING unit >= 100
```
