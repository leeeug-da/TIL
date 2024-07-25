### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기)
- *table* : CAR_RENTAL_COMPANY_RENTAL_HISTORY

<br>

**CAR_RENTAL_COMPANY_RENTAL_HISTORY**
|column|type|nullable|
|---|---|---|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER|	FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블입니다. `CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블은 아래와 같은 구조로 되어있으며, `HISTORY_ID`, `CAR_ID`, `START_DATE`, `END_DATE` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

<br>

### Problem 
`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블에서 대여 시작일을 기준으로 2022년 8월부터 2022년 10월까지 총 대여 횟수가 5회 이상인 자동차들에 대해서 해당 기간 동안의 월별 자동차 ID 별 총 대여 횟수(컬럼명: `RECORDS`) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 월을 기준으로 오름차순 정렬하고, 월이 같다면 자동차 ID를 기준으로 내림차순 정렬해주세요. 특정 월의 총 대여 횟수가 0인 경우에는 결과에서 제외해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_RENTAL_HISTORY*

|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	1|	2022-07-27|	2022-08-02|
|2|	1|	2022-08-03|	2022-08-04|
|3|	2|	2022-08-05|	2022-08-05|
|4|	2|	2022-08-09|	2022-08-12|
|5|	3|	2022-09-16|	2022-10-15|
|6|	1|	2022-08-24|	2022-08-30|
|7|	3|	2022-10-16|	2022-10-19|
|8|	1|	2022-09-03|	2022-09-07|
|9|	1|	2022-09-18|	2022-09-19|
|10|	2|	2022-09-08|	2022-09-10|

<br>

**Sample Output**

|MONTH|	CAR_ID|	RECORDS|
|---|---|---|
|8|	2|	2|
|8|	1|	2|
|9|	2|	1|
|9|	1|	3|
|10|	2|	2|

<br>

### Solving

```sql
SELECT MONTH(START_DATE) AS MONTH
     , CAR_ID
     , COUNT(CAR_ID) AS RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
  AND CAR_ID IN (SELECT CAR_ID
                 FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                 WHERE START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
                 GROUP BY CAR_ID
                 HAVING COUNT(CAR_ID) >= 5)
GROUP BY MONTH(START_DATE), CAR_ID
ORDER BY MONTH ASC, CAR_ID DESC
```
