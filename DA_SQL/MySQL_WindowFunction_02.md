### Topic
- Window Function (FRAME)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql (누적 합 계산하기)
- *table* : measurements

**measurements**
|column|type|
|---|---|
|measured_at|date|
|station|string|
|no2|number|
|o3|number|
|co|number|
|so2|number|
|pm10|number|
|pm2_5|number|


<br>

### Problem 
서울숲 일별 평균 대기오염도 데이터로 누적 합을 계산해 주세요

<br>

**Sample Input**
|measured_at|station|no2|o3|co|so2|pm10|pm2_5|
|---|---|---|---|---|---|---|---|
|2022-01-01|서울숲|0.034|0.012|0.6|0.004|31|12|
|2022-01-02|서울숲|0.027|0.016|0.6|0.004|39|23|
|2022-01-03|서울숲|0.039|0.007|0.7|0.004|28|14|
|2022-01-04|서울숲|0.027|0.015|0.7|0.004|37|20|

<br>

**Sample Output**
|measured_at|pm10|pm10_running_total|
|---|---|---|
|2022-01-01|31|31|
|2022-01-02|39|70|
|2022-01-03|28|98|
|2022-01-04|37|135|


<br>

### Solving
```sql
SELECT measured_at
     , pm10
     , SUM(pm10) OVER (ORDER BY measured_at ROWS UNBOUNDED PRECEDING) AS pm10_running_total
FROM measurements
ORDER BY measured_at
```
