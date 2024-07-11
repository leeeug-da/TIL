### Topic
- Window Function (LEAD, LAG)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql (다음날도 서울숲의 미세먼지 농도는 나쁨 😢)
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
서울숲 일별 평균 대기오염도 데이터셋은 2022년 서울숲 대기오염도 측정소에서 매일 기록한 대기오염 정보를 담고 있습니다.
`measurements` 테이블의 `pm10` 컬럼에는 다양한 대기오염도 측정 기준 중에서도 미세먼지(PM10) 농도가 기록되어 있습니다. 이 데이터를 이용하여 당일의 미세먼지 농도보다 바로 다음날의 미세먼지 농도가 더 안좋은 날을 찾아주세요. 결과는 아래 컬럼들을 포함해야 합니다.
- `today`: 당일 (YYYY-MM-DD)
- `next_day`: 다음날 (YYYY-MM-DD)
- `pm10`: 당일의 미세먼지 농도
- `next_pm10`: 다음날의 미세먼지 농도

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
|today|next_day|pm10|next_pm10|
|---|---|---|---|
|2022-01-01|2022-01-02|31|39|
|2022-01-03|2022-01-04|28|37|
|2022-01-04|2022-01-05|37|52|
|2022-01-05|2022-01-06|52|56|


<br>

### Solving
```sql
SELECT *
FROM (
  SELECT measured_at AS today
      , LEAD(measured_at) OVER (ORDER BY measured_at) AS next_day
      , pm10
      , LEAD(pm10) OVER (ORDER BY measured_at) AS next_pm10
  FROM measurements
) next_pm
WHERE pm10 < next_pm10
```
