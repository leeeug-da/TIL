### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : LeetCode (585. Investments in 2016)
- *table* : Insurance

**Seat**
|column|type|
|---|---|
| pid         | int   |
| tiv_2015    | float |
| tiv_2016    | float |
| lat         | float |
| lon         | float |

pid is the primary key (column with unique values) for this table.

Each row of this table contains information about one policy where:
pid is the policyholder's policy ID.

tiv_2015 is the total investment value in 2015 and tiv_2016 is the total investment value in 2016.

lat is the latitude of the policy holder's city. It's guaranteed that lat is not NULL.

lon is the longitude of the policy holder's city. It's guaranteed that lon is not NULL.


<br>

### Problem 
Write a solution to report the sum of all total investment values in 2016 `tiv_2016`, for all policyholders who:
- have the same `tiv_2015` value as one or more other policyholders, and
- are not located in the same city as any other policyholder (i.e., the (`lat`, `lon`) attribute pairs must be unique).
Round `tiv_2016` to two decimal places.



<br>

**Sample Input**
| pid | tiv_2015 | tiv_2016 | lat | lon |
|---|---|---|---|---|
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |

<br>

**Sample Output**
| tiv_2016 |
|---|
| 45.00    |
<br>

### Solving
```sql
WITH CTE AS (
SELECT pid
     , tiv_2015
     , tiv_2016
     , COUNT(tiv_2015) OVER (PARTITION BY tiv_2015) AS cnt_tiv_2015
     , COUNT(CONCAT(lat,lon)) OVER (PARTITION BY CONCAT(lat,lon)) AS cnt_city
FROM Insurance
)

SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM CTE
WHERE cnt_tiv_2015 > 1  -- Same tiv_2015 as one or more other policyholders
  AND cnt_city = 1      -- Unique (lat, lon)
```
