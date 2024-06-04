### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (570. Managers with at Least 5 Direct Reports)
- *table* : Employee

**Employee**
|column|type|
|---|---|
|id|int|
|name|varchar|
|department|varchar|
|managerId|int|

id is the primary key (column with unique values) for this table.
Each row of this table indicates the name of an employee, their department, and the id of their manager.
If managerId is null, then the employee does not have a manager.
No employee will be the manager of themself.



### Problem 
Write a solution to find managers with at least five direct reports.

Return the result table in any order.

The result format is in the following example.



**Sample Input**

*Employee*
|id|name|department|managerId
|---|---|---|---|
|101|John|A|null|
|102|Dan|A|101|
|103|James|A|101|
|104|Amy|A|101|
|105|Anne|A|101|
|106|Ron|B|101|



**Sample Output**

|name|
|---|
|John|


### Solving

```sql
SELECT E.name
FROM Employee E
 JOIN Employee M ON M.managerId = E.id
GROUP BY M.managerId
HAVING COUNT(M.managerId) >= 5
```
