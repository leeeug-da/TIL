### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (176. Second Highest Salary)
- *table* : Employee

**Employee**
|column|type|
|---|---|
| id          | int  |
| salary      | int  |

id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.


<br>

### Problem 
Write a solution to find the second highest distinct salary from the `Employee` table. If there is no second highest salary, return `null` (return None in Pandas).



<br>

### Example 1

**Sample Input**
| id | salary |
|---|---|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |



**Sample Output**
| SecondHighestSalary |
|---|
| 200                 |

<br>

### Example 2

**Sample Input**
| id | salary |
|---|---|
| 1  | 100    |


**Sample Output**
| SecondHighestSalary |
|---|
| null                |


<br>

### Solving
```sql
WITH srank AS (
    SELECT id, salary
        , DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rk
    FROM Employee
)

SELECT MAX(CASE
            WHEN salary_rk = 2 THEN salary
            ELSE null
            END) AS SecondHighestSalary
FROM srank
LIMIT 1
```
