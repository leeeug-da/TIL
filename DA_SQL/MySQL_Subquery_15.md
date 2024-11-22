### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (1978. Employees Whose Manager Left the Company)
- *table* : Employees

<br>

**Employees**
|column|type|
|---|---|
| employee_id | int      |
| name        | varchar  |
| manager_id  | int      |
| salary      | int      |

In SQL, employee_id is the primary key for this table.
This table contains information about the employees, their salary, and the ID of their manager. Some employees do not have a manager (manager_id is null).

<br>

### Problem 
Find the IDs of the employees whose salary is strictly less than `$30000` and whose manager left the company. When a manager leaves the company, their information is deleted from the `Employees` table, but the reports still have their `manager_id` set to the manager that left.

Return the result table ordered by `employee_id`.

The result format is in the following example.

<br>

**Sample Input**

*Employees*
| employee_id | name      | manager_id | salary |
|---|---|---|---|
| 3           | Mila      | 9          | 60301  |
| 12          | Antonella | null       | 31000  |
| 13          | Emery     | null       | 67084  |
| 1           | Kalel     | 11         | 21241  |
| 9           | Mikaela   | null       | 50937  |
| 11          | Joziah    | 6          | 28485  |

<br>

**Sample Output**
| employee_id |
|---|
| 11          |


<br>

### Solving
```sql
SELECT employee_id
FROM Employees
WHERE manager_id NOT IN (SELECT employee_id
                         FROM Employees)
  AND salary < 30000
ORDER BY employee_id
```
