### Topic
- Select
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (1757. Recyclable and Low Fat Products)
- *table* : Products

**Products**
|column|type|
|---|---|
|product_id|int|
|low_fats|enum|
|recyclable|enum|

product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.

### Problem 
Write a solution to find the ids of products that are both low fat and recyclable.

Return the result table in any order.

The result format is in the following example.

**Sample Input**

*Products*
|product_id|low_fats|recyclable|
|---|---|---|
|0|Y|N|
|1|Y|Y|
|2|N|Y|


**Sample Output**

|product_id|
|---|
|1|
|3|

### Solving

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y'
```

