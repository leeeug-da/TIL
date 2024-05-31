### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (262. Trips and Users)
- *table* : Trips, Users

**Trips**
|column|type|
|---|---|
|id|int|
|client_id|int|
|driver_id|int|
|city_id|int|
|status|enum|
|request_at|date|

id is the primary key (column with unique values) for this table.
The table holds all taxi trips. Each trip has a unique id, while client_id and driver_id are foreign keys to the users_id at the Users table.
Status is an ENUM (category) type of ('completed', 'cancelled_by_driver', 'cancelled_by_client').

**Users**
|column|type|
|---|---|
|users_id|int|
|banned|enum|
|role|enum|

users_id is the primary key (column with unique values) for this table.
The table holds all users. Each user has a unique users_id, and role is an ENUM type of ('client', 'driver', 'partner').
banned is an ENUM (category) type of ('Yes', 'No').


### Problem 
The cancellation rate is computed by dividing the number of canceled (by client or driver) requests with unbanned users by the total number of requests with unbanned users on that day.

Write a solution to find the cancellation rate of requests with unbanned users (both client and driver must not be banned) each day between "2013-10-01" and "2013-10-03". Round Cancellation Rate to two decimal points.

Return the result table in any order.

The result format is in the following example.


**Sample Output**
|Day|Cancellation Rate|
|---|---|
|2013-10-01|0.33|
|2013-10-02|0.00|
|2013-10-03|0.50|


### Solving
```sql
SELECT request_at AS Day
     , ROUND(SUM(
        IF(status = 'completed', 0, 1))/COUNT(status), 2) AS 'Cancellation Rate' 
FROM Trips 
WHERE client_id NOT IN (SELECT users_id FROM Users WHERE banned = 'Yes') 
    AND driver_id NOT IN (SELECT users_id FROM Users WHERE banned = 'Yes')
    AND request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY request_at;
```
