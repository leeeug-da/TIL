### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (184. Department Highest Salary)
- *table* : Employee, Department

**Employee**
|column|type|
|---|---|
|id|int|
|name|varchar|
|salary|int|
|departmentId|int|

id is the primary key (column with unique values) for this table.
departmentId is a foreign key (reference columns) of the ID from the `Department` table.
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.

**Department**
|column|type|
|---|---|
|id|int|
|name|varchar|

id is the primary key (column with unique values) for this table. It is guaranteed that department name is not `NULL`.
Each row of this table indicates the ID of a department and its name.


### Problem 
Write a solution to find employees who have the highest salary in each of the departments.

Return the result table in any order.

The result format is in the following example.

**Sample Input**

*Employee table:*

|id|name|salary|departmentId|
|---|---|---|---|
|1|Joe|70000|1|
|2|Jim|90000|1|
|3|Henry|80000|2|
|4|Sam|60000|2|
|5|Max|90000|1|

*Department table:*

|id|name|
|---|---|
|1|IT|
|2|Sales|

<br>

**Sample Output**
|Department|Employee|Salary|
|---|---|---|
|IT|Jim|90000|
|Sales|Henry|80000|
|IT|Max|90000|


### Solving
```sql
SELECT D.name AS Department
     , E.name AS Employee
     , E.salary AS Salary 
FROM Employee E
  JOIN Department D ON D.id = E.departmentId
WHERE E.salary = (SELECT MAX(salary)
                  FROM Employee E2
                  WHERE E2.departmentId = E.departmentId)
```
