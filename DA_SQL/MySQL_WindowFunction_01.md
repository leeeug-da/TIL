### Topic
- Window Function
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (511. Game Play Analysis I)
- *table* : Activity

**Activity**
|column|type|
|---|---|
|player_id|int|
|device_id|int|
|event_date|date|
|games_played|int|

(player_id, event_date) is the primary key (combination of columns with unique values) of this table.
This table shows the activity of players of some games.
Each row is a record of a player who logged in and played a number of games (possibly 0) before logging out on someday using some device.

<br>

### Problem 
Write a solution to find the first login date for each player.

Return the result table in any order.

The result format is in the following example.

<br>

**Sample Input**

*Activity*
| player_id | device_id | event_date | games_played |
|---|---|---|---|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-05-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |

<br>

**Sample Output**
| player_id | first_login |
|---|---|
| 1         | 2016-03-01  |
| 2         | 2017-06-25  |
| 3         | 2016-03-02  |


<br>

### Solving
```sql
SELECT player_id
     , event_date as first_login
FROM (
 SELECT player_id
     , event_date
     , ROW_NUMBER() OVER (PARTITION BY player_id ORDER BY event_date ASC) AS row_n
 FROM Activity
 ) player_row_n
WHERE row_n = 1
```
