### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Placements)
- *table* : Students, Friends, Packages

**Students**
|column|type|
|---|---|
|ID|Integer|
|Name|String|

**Friends**
|column|type|
|---|---|
|ID|Integer|
|Friend_ID|Integer|

**Packages**
|column|type|
|---|---|
|ID|Integer|
|Salary|Float|




### Problem 
You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month).

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

**Sample Input**

*Friends*
|ID|Friend_ID|
|---|---|
|1|2|
|2|3|
|3|4|
|4|1|

*Students*
|ID|Name|
|---|---|
|1|Ashley|
|2|Samantha|
|3|Julia|
|4|Scarlet|

*Packages*
|ID|Salary|
|---|---|
|1|15.20|
|2|10.06|
|3|11.55|
|4|12.12|


**Sample Output**

Samantha <br>
Julia <br>
Scarlet <br>


### Solving

```sql
SELECT s.Name
FROM Students AS s
    JOIN Packages AS p1 ON s.ID = p1.ID
    JOIN Friends AS f ON s.ID = f.ID
    JOIN Packages AS p2 ON f.Friend_ID = p2.ID
WHERE p1.salary < p2.salary
ORDER BY p2.salary;
```
