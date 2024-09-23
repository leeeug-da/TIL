### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (연도 별 평균 미세먼지 농도 조회하기)
- *table* : AIR_POLLUTION

<br>

**AIR_POLLUTION**
|column|type|nullable|
|---|---|---|
|LOCATION1|	VARCHAR|	FALSE|
|LOCATION2|	VARCHAR|	FALSE|
|YM|	DATE|	FALSE|
|PM_VAL1|	NUMBER|	FLASE|
|PM_VAL2|	NUMBER|	FLASE|

`AIR_POLLUTION` 테이블의 구조는 다음과 같으며 `LOCATION1`, `LOCATION2`, `YM`, `PM_VAL1`, `PM_VAL2`은 각각 지역구분1, 지역구분2, 측정일, 미세먼지 오염도, 초미세먼지 오염도를 의미합니다.

<br>

### Problem
`AIR_POLLUTION` 테이블에서 수원 지역의 연도 별 평균 미세먼지 오염도와 평균 초미세먼지 오염도를 조회하는 SQL문을 작성해주세요. 이때, 평균 미세먼지 오염도와 평균 초미세먼지 오염도의 컬럼명은 각각 PM10, PM2.5로 해 주시고, 값은 소수 셋째 자리에서 반올림해주세요.
결과는 연도를 기준으로 오름차순 정렬해주세요.



<br>

**Sample Input**

*AIR_POLLUTION*
|LOCATION1|	LOCATION2|	YM|	PM_VAL1|	PM_VAL2|
|---|---|---|---|---|
|경기도|	수원|	2018-01-01|	48|	27|
|경기도|	수원|	2018-02-01|	51|	30|
|경기도|	수원|	2018-03-01|	52|	21|
|경기도|	수원|	2018-04-01|	52|	20|
|서울시|	노원|	2018-11-01|	25|	45|
  
<br>

**Sample Output**

|YEAR|	PM10|	PM2.5|
|---|---|---|
|2018|	41|	20.25|

<br>

### Solving

```sql
SELECT YEAR(YM) AS YEAR
     , ROUND(AVG(PM_VAL1), 2) AS 'PM10'
     , ROUND(AVG(PM_VAL2), 2) AS 'PM2.5'
FROM AIR_POLLUTION
WHERE LOCATION2 = '수원'
GROUP BY YEAR
ORDER BY YEAR
```
