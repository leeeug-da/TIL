### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (181. Employees Earning More Than Their Managers)
- *table* : Employee

|column|type|
|---|---|
|id|int|
|name|varchar|
|salary|int|
|managerId|int|

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID of an employee, their name, salary, and the ID of their manager.


### Problem 
Write a solution to find the employees who earn more than their managers.

Return the result table in any order.

The result format is in the following example.

**Sample Input**
|id|name|salary|managerId|
|---|---|---|---|
|1|Joe|70000|3|
|2|Henry|80000|4|
|3|Sam|60000|Null|
|4|Max|90000|Null|

**Sample Output**
|Employee|
|---|
|Joe|


### Solving
```sql
SELECT name AS Employee
FROM Employee E
WHERE E.salary > (SELECT salary
                  FROM Employee E2
                  WHERE E2.id = E.managerId)
```
