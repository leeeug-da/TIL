### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (1045. Customers Who Bought All Products)
- *table* : Customer, Product

**Customer**
|column|type|
|---|---|
|custoer_id|int|
|product_key|int|

This table may contain duplicates rows. 
customer_id is not NULL.
product_key is a foreign key (reference column) to Product table.

**Product**
|column|type|
|---|---|
|product_key|int|

product_key is the primary key (column with unique values) for this table.

### Problem 
Write a solution to report the customer ids from the Customer table that bought all the products in the Product table.

Return the result table in any order.

The result format is in the following example.




**Sample Input**

*Customer table:*
|customer_id|product_key|
|---|---|
|1|5|
|2|6|
|3|5|
|3|6|
|1|6|

*Product table:*
|product_key|
|---|
|5|
|6|

<br>

**Sample Output**
|customer_id|
|---|
|1|
|3|

<br>

### Solving
```sql
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(product_key)
                                      FROM Product)
```
