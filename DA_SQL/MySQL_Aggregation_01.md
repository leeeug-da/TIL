### Topic
- Aggregation
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Top earners)
- *table* : Employee

|column|type|description|  
|---|---|---|
|integer|employee_id|employee's id number|
|string|name|employee's name|
|integer|months|total number of months employee has been working|
|integer|salary|monthly salary|




### Problem 
We define an employee's total earnings to be their monthly  worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.

**Sample Input**
|employee_id|name|months|salary|
|---|---|---|---|
|12228|Rose|15|1968|
|33645|Angela|1|3443|
|45692|Frank|17|1608|
|56118|Patrick|7|1345|
|59725|Lisa|11|2330|
|74197|Kimberly|16|4372|
|78454|Bonnie|8|1771|
|83565|Michael|6|2017|12102|
|98607|Todd|5|3396|
|99989|Joe|9|3573|

**Sample Output**

69952 1


**Explanation**

The maximum earnings value is . The only employee with earnings  is Kimberly, so we print the maximum earnings value () and a count of the number of employees who have earned  (which is ) as two space-separated values.


### Solving

```sql
SELECT 
      salary * months AS total_earnings
    , COUNT(DISTINCT(employee_id)) AS max_employee
FROM Employee
GROUP BY total_earnings
ORDER BY total_earnings DESC
LIMIT 1;
```

