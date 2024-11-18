### Topic
- REGEXP (정규표현식)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (1484. Group Sold Products By The Date)
- *table* : Activities

**Activities**
|column|type|
|---|---|
| sell_date   | date    |
| product     | varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.
Each row of this table contains the product name and the date it was sold in a market.


<br>

### Problem 
Write a solution to find for each date the number of different products sold and their names.

The sold products names for each date should be sorted lexicographically.

Return the result table ordered by `sell_date`.

<br>

**Sample Input**
| sell_date  | product     |
|---|---|
| 2020-05-30 | Headphone  |
| 2020-06-01 | Pencil     |
| 2020-06-02 | Mask       |
| 2020-05-30 | Basketball |
| 2020-06-01 | Bible      |
| 2020-06-02 | Mask       |
| 2020-05-30 | T-Shirt    |

<br>

**Sample Output**
| sell_date  | num_sold | products                     |
|---|---|---|
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |


<br>

### Solving
```sql
SELECT sell_date
     , COUNT(DISTINCT product) AS num_sold
     , GROUP_CONCAT(DISTINCT product ORDER BY product) AS products
FROM Activities
GROUP BY sell_date
ORDER BY sell_date
```
