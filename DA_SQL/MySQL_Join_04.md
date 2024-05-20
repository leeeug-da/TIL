### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (The Report)
- *table* : Students, Grades

**Students**
|column|type|
|---|---|
|ID|Integer|
|Name|String|
|Marks|Integer|

**COUNTRY**
|column|type|
|---|---|
|Grade|Integer|
|Min_Mark|Integer|
|Max_Mark|Integer|




### Problem 
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

**Sample Input**
|ID|Name|Marks|
|---|---|---|
|1|Julia|88|
|2|Samantha|68|
|3|Maria|99|
|4|Scarlet|78|
|5|Ashley|63|
|6|Jane|81|

**Sample Output**

Maria 10 99 <br>
Jane 9 81 <br>
Julia 9 88 <br>
Scarlet 8 78 <br>
NULL 7 63 <br>
NULL 7 68 <br>


### Solving

```sql
SELECT CASE
            WHEN g.Grade >= 8 THEN s.NAME
            ELSE 'NULL'
       END 
     , g.Grade
     , s.Marks
FROM Students s
    JOIN Grades g ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark 
ORDER BY g.Grade DESC, s.NAME ASC, s.Marks ASC;
```

### Study Note
- Join 조건으로 범위 (BETWEEN) 사용이 가능하다.
    ```sql
    FROM Students s
    JOIN Grades g ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark 
    ```

- ORDER BY 컬럼 순서를 어떻게 하냐에 따라 결과가 다르게 나온다.
  - 틀린 예시:
    ```sql
    ORDER BY g.Grade DESC, s.Marks ASC, s.NAME ASC;
    ```
  - 정답 예시:
    ```sql
    ORDER BY g.Grade DESC, s.NAME ASC, s.Marks ASC;
    ```
