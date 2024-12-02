### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (1321. Restaurant Growth)
- *table* : Customer

<br>

**Customer**
|column|type|
|---|---|
| customer_id   | int     |
| name          | varchar |
| visited_on    | date    |
| amount        | int     |

In SQL,(customer_id, visited_on) is the primary key for this table.
This table contains data about customer transactions in a restaurant.
visited_on is the date on which the customer with ID (customer_id) has visited the restaurant.
amount is the total paid by a customer.

<br>

### Problem 
You are the restaurant owner and you want to analyze a possible expansion (there will be at least one customer every day).

Compute the moving average of how much the customer paid in a seven days window (i.e., current day + 6 days before). `average_amount` should be rounded to two decimal places.

Return the result table ordered by `visited_on` in ascending order.

<br>

**Sample Input**

| customer_id | name         | visited_on   | amount      |
|---|---|---|---|
| 1           | Jhon         | 2019-01-01   | 100         |
| 2           | Daniel       | 2019-01-02   | 110         |
| 3           | Jade         | 2019-01-03   | 120         |
| 4           | Khaled       | 2019-01-04   | 130         |
| 5           | Winston      | 2019-01-05   | 110         | 
| 6           | Elvis        | 2019-01-06   | 140         | 
| 7           | Anna         | 2019-01-07   | 150         |
| 8           | Maria        | 2019-01-08   | 80          |
| 9           | Jaze         | 2019-01-09   | 110         | 
| 1           | Jhon         | 2019-01-10   | 130         | 
| 3           | Jade         | 2019-01-10   | 150         | 

<br>

**Sample Output**
| visited_on   | amount       | average_amount |
|---|---|---|
| 2019-01-07   | 860          | 122.86         |
| 2019-01-08   | 840          | 120            |
| 2019-01-09   | 840          | 120            |
| 2019-01-10   | 1000         | 142.86         |


<br>

### Solving
```sql
SELECT
    visited_on,
    (SELECT SUM(amount)
     FROM customer
     WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
    ) AS amount,
    ROUND((SELECT SUM(amount) / 7
           FROM customer
           WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on), 2
    ) AS average_amount
FROM Customer C
WHERE visited_on >= (SELECT DATE_ADD(MIN(visited_on), INTERVAL 6 DAY)
                     FROM customer)
GROUP BY visited_on;
```
