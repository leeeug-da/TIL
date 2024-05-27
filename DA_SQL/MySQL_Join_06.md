### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (Customers Who Never Order)
- *table* : Customers, Orders

**Customers**
|column|type|
|---|---|
|id|int|
|name|varchar|

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID and name of a customer.

**Orders**
|column|type|
|---|---|
|id|int|
|customerId|int|

id is the primary key (column with unique values) for this table.
customerId is a foreign key (reference columns) of the ID from the Customers table.
Each row of this table indicates the ID of an order and the ID of the customer who ordered it.





### Problem 
Write a solution to find all customers who never order anything.

Return the result table in any order.



**Sample Input**

*Customers*
|id|name|
|---|---|
|1|Joe|
|2|Henry|
|3|Sam|
|4|Max|

*Orders*
|id|customerId|
|---|---|
|1|3|
|2|1|



**Sample Output**

|Customers|
|---|
|Henry|
|Max|


### Solving

```sql
SELECT c.name AS Customers
FROM Customers c
 LEFT JOIN Orders o ON o.customerId = c.id
WHERE o.id IS NULL
```
