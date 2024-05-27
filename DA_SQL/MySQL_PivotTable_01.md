### Topic
- Pivot Table 
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (1179. Reformat Department Table)
- *table* : Department

| Column Name | Type    |
|---|---|
| id          | int     |
| revenue     | int     |
| month       | varchar |

<br>
In SQL,(id, month) is the primary key of this table. <br>
The table has information about the revenue of each department per month. <br>
The month has values in ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"].


<br>

### Problem 
Reformat the table such that there is a department id column and a revenue column for each month.
Return the result table in any order.
The result format is in the following example.

**Sample Input**

| id   | revenue | month |
|---|---|---|
| 1    | 8000    | Jan   |
| 2    | 9000    | Jan   |
| 3    | 10000   | Feb   |
| 1    | 7000    | Feb   |
| 1    | 6000    | Mar   |


**Sample Output**

| id   | Jan_Revenue | Feb_Revenue | Mar_Revenue | ... | Dec_Revenue |
|---|---|---|---|---|---|
| 1    | 8000        | 7000        | 6000        | ... | null        |
| 2    | 9000        | null        | null        | ... | null        |
| 3    | null        | 10000       | null        | ... | null        |

<br>

### Solving
```sql
SELECT id
     , SUM(CASE WHEN month = 'Jan' THEN revenue END) AS 'Jan_Revenue'
     , SUM(CASE WHEN month = 'Feb' THEN revenue END) AS 'Feb_Revenue'
     , SUM(CASE WHEN month = 'Mar' THEN revenue END) AS 'Mar_Revenue'
     , SUM(CASE WHEN month = 'Apr' THEN revenue END) AS 'Apr_Revenue'
     , SUM(CASE WHEN month = 'May' THEN revenue END) AS 'May_Revenue'
     , SUM(CASE WHEN month = 'Jun' THEN revenue END) AS 'Jun_Revenue'
     , SUM(CASE WHEN month = 'Jul' THEN revenue END) AS 'Jul_Revenue'
     , SUM(CASE WHEN month = 'Aug' THEN revenue END) AS 'Aug_Revenue'
     , SUM(CASE WHEN month = 'Sep' THEN revenue END) AS 'Sep_Revenue'
     , SUM(CASE WHEN month = 'Oct' THEN revenue END) AS 'Oct_Revenue'
     , SUM(CASE WHEN month = 'Nov' THEN revenue END) AS 'Nov_Revenue'
     , SUM(CASE WHEN month = 'Dec' THEN revenue END) AS 'Dec_Revenue'
FROM Department
GROUP BY id
```
