### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (180. Consecutive Numbers)
- *table* : Logs

**Seat**
|column|type|
|---|---|
| id          | int     |
| num         | varchar |


<br>

### Problem 
Find all numbers that appear at least three times consecutively.

Return the result table in any order.



<br>

**Sample Input**
| id | num |
|---|---|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

<br>

**Sample Output**
| ConsecutiveNums |
|---|
| 1               |

<br>

### Solving
```sql
SELECT DISTINCT(num) AS ConsecutiveNums
FROM (
    SELECT id, num
         , LAG(num) OVER (ORDER BY id) AS prev
         , LEAD(num) OVER (ORDER BY id) AS after
    FROM Logs
) x
WHERE x.num = x.prev AND x.prev = x.after
```
