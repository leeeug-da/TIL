### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (1731. The Number of Employees Which Report to Each Employee)
- *table* : Employees

**Signups**
|column|type|
|---|---|
|employee_id|int|
|name|varchar|
|reports_to|int|
|age|int|

employee_id is the column with unique values for this table.
This table contains information about the employees and the id of the manager they report to. Some employees do not report to anyone (reports_to is null). 




### Problem 
For this problem, we will consider a manager an employee who has at least 1 other employee reporting to them.

Write a solution to report the ids and the names of all managers, the number of employees who report directly to them, and the average age of the reports rounded to the nearest integer.

Return the result table ordered by employee_id.

The result format is in the following example.



**Sample Input**

| employee_id | name    | reports_to | age |
|---|---|---|---|
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |




**Sample Output**

| employee_id | name  | reports_count | average_age |
|---|---|---|---|
| 9           | Hercy | 2             | 39          |


### Solving

```sql
SELECT E1.employee_id
     , E1.name
     , COUNT(E2.employee_id) AS reports_count
     , ROUND(AVG(E2.age)) AS average_age
FROM Employees E1
 JOIN Employees E2 ON E2.reports_to = E1.employee_id
GROUP BY employee_id
ORDER BY employee_id
```
