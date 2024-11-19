### Topic
- REGEXP (정규표현식)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (1667. Fix Names in a Table)
- *table* : Users

**Users**
|column|type|
|---|---|
| user_id        | int     |
| name           | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains the ID and the name of the user. The name consists of only lowercase and uppercase characters.



<br>

### Problem 
Write a solution to fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by `user_id`.

<br>

**Sample Input**
| user_id | name  |
|---|---|
| 1       | aLice |
| 2       | bOB   |

<br>

**Sample Output**
| user_id | name  |
|---|---|
| 1       | Alice |
| 2       | Bob   |


<br>

### Solving
```sql
SELECT user_id
     , CONCAT(UPPER(SUBSTR(name,1,1)), LOWER(SUBSTR(name,2))) AS name
FROM Users
ORDER BY user_id
```
