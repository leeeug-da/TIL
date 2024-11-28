### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (602. Friend Requests II: Who Has the Most Friends)
- *table* : RequestAccepted

<br>

**RequestAccepted**
|column|type|
|---|---|
| requester_id   | int     |
| accepter_id    | int     |
| accept_date    | date    |

(requester_id, accepter_id) is the primary key (combination of columns with unique values) for this table.
This table contains the ID of the user who sent the request, the ID of the user who received the request, and the date when the request was accepted.

<br>

### Problem 
Write a solution to find the people who have the most friends and the most friends number.

The test cases are generated so that only one person has the most friends.

<br>

**Sample Input**

| requester_id | accepter_id | accept_date |
|---|---|---|
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |

<br>

**Sample Output**
| id | num |
|---|---|
| 3  | 3   |


<br>

### Solving
```sql
WITH CTE AS (
SELECT requester_id AS id FROM RequestAccepted
UNION ALL
SELECT accepter_id AS id FROM RequestAccepted
)

SELECT id
     , COUNT(id) AS num
FROM CTE
GROUP BY id
ORDER BY num DESC
LIMIT 1
```
