### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (1084. Sales Analysis III)
- *table* : Product, Sales

**Product**
|column|type|
|---|---|
|product_id|int|
|product_name|varchar|
|unit_price|int|

product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the name and the price of each product.

**Sales**
|column|type|
|---|---|
|seller_id|int|
|product_id|int|
|buyer_id|int|
|sale_date|date|
|quantity|int|
|price|int|

This table can have duplicate rows.
product_id is a foreign key (reference column) to the Product table.
Each row of this table contains some information about one sale.



### Problem 
Write a solution to report the products that were only sold in the first quarter of 2019. That is, between `2019-01-01` and `2019-03-31` inclusive.

Return the result table in any order.

The result format is in the following example.



**Sample Input**

*Product*
|product_id|product_name|unit_price|
|---|---|---|
|1|S8|1000|
|2|G4|800|
|3|iPhone|1400|

*Sales*
|seller_id|product_id|buyer_id|sale_date|quantity|price|
|---|---|---|---|---|---|
|1|1|1|2019-01-21|2|2000|
|1|2|2|2019-02-17|1|800|
|2|2|3|2019-06-02|1|800|
|3|3|4|2019-05-13|2|2800|


**Sample Output**

|product_id|product_name|
|---|---|
|1|S8|


### Solving

```sql
SELECT DISTINCT P.product_id
      , P.product_name
FROM Sales S
  JOIN Product P ON P.product_id = S.product_id
GROUP BY P.product_id
HAVING MIN(sale_date) >= '2019-01-01' 
   AND MAX(sale_date) <= '2019-03-31'
```
