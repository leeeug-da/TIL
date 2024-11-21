### Topic
- DELETE
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (196. Delete Duplicate Emails)
- *table* : Person

**Users**
|column|type|
|---|---|
| id          | int     |
| email       | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table contains an email. The emails will not contain uppercase letters.


<br>

### Problem 
Write a solution to delete all duplicate emails, keeping only one unique email with the smallest `id`.

For SQL users, please note that you are supposed to write a `DELETE` statement and not a `SELECT` one.

After running your script, the answer shown is the Person table. The driver will first compile and run your piece of code and then show the Person table. The final order of the Person table does not matter.





<br>

**Sample Input**
| id | email            |
|---|---|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

<br>

**Sample Output**
| id | email            |
|---|---|
| 1  | john@example.com |
| 2  | bob@example.com  |


<br>

### Solving
```sql
DELETE A
FROM Person A
 JOIN Person B 
WHERE A.id > B.id 
  AND B.email = A.email 
```
