### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (626. Exchange Seats)
- *table* : Seat

**Seat**
|column|type|
|---|---|
| id          | int     |
| student     | varchar |

id is the primary key (unique value) column for this table.
Each row of this table indicates the name and the ID of a student.
The ID sequence always starts from 1 and increments continuously.


<br>

### Problem 
Write a solution to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.

Return the result table ordered by `id` in ascending order.

<br>

**Sample Input**
| id | student |
|---|---|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

<br>

**Sample Output**
| id | student |
|---|---|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

<br>

### Solving
```sql
SELECT id
     , CASE
        WHEN id%2 = 0 THEN LAG(student, 1) OVER (ORDER BY id)
        ELSE IFNULL(LEAD(student, 1) OVER (ORDER BY id), student)
       END AS student
FROM Seat
```
