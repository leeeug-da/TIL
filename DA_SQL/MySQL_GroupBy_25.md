### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (GROUP BY) (2356. Number of Unique Subjects Taught by Each Teacher)
- *table* : Teacher

<br>

**Teacher**
|column|type|
|---|---|
| teacher_id  | int  |
| subject_id  | int  |
| dept_id     | int  |

(subject_id, dept_id) is the primary key (combinations of columns with unique values) of this table.
Each row in this table indicates that the teacher with teacher_id teaches the subject subject_id in the department dept_id.

<br>

### Problem
Write a solution to calculate the number of unique subjects each teacher teaches in the university.

Return the result table in any order.

<br>

**Sample Input**

| teacher_id | subject_id | dept_id |
|---|---|---|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |

<br>

**Sample Output**

| teacher_id | cnt |
|---|---|
| 1          | 2   |
| 2          | 4   |

<br>

### Solving

```sql
SELECT teacher_id
     , COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id
```
