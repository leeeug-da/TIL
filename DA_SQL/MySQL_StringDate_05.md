### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (자동차 대여 기록에서 장기/단기 대여 구분하기)
- *table* : CAR_RENTAL_COMPANY_RENTAL_HISTORY

<br>

**CAR_RENTAL_COMPANY_RENTAL_HISTORY**
|column|type|nullable|
|---|---|---|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER|	FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블은 아래와 같은 구조로 되어있으며, `HISTORY_ID`, `CAR_ID`, `START_DATE`, `END_DATE` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

<br>

### Problem
`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블에서 대여 시작일이 2022년 9월에 속하는 대여 기록에 대해서 대여 기간이 30일 이상이면 '장기 대여' 그렇지 않으면 '단기 대여' 로 표시하는 컬럼(컬럼명: `RENT_TYPE`)을 추가하여 대여기록을 출력하는 SQL문을 작성해주세요. 결과는 대여 기록 ID를 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_RENTAL_HISTORY*
|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	4|	2022-09-27|	2022-11-27|
|2|	3|	2022-10-03|	2022-11-04|
|3|	2|	2022-09-05|	2022-09-05|
|4|	1|	2022-09-01|	2022-09-30|
|5|	3|	2022-09-16|	2022-10-15|
  
<br>

**Sample Output**

|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|RENT_TYPE|
|---|---|---|---|---|
|1|	4|	2022-09-27|	2022-11-27|장기 대여|
|3|	2|	2022-09-05|	2022-09-05|단기 대여|
|4|	1|	2022-09-01|	2022-09-30|장기 대여|
|5|	3|	2022-09-16|	2022-10-15|단기 대여|

<br>

### Solving

```sql
SELECT HISTORY_ID, CAR_ID
     , DATE_FORMAT(START_DATE, '%Y-%m-%d') AS START_DATE
     , DATE_FORMAT(END_DATE, '%Y-%m-%d') AS END_DATE
     , CASE
            WHEN (DATEDIFF(END_DATE, START_DATE)+1) >= 30 THEN '장기 대여'
            ELSE '단기 대여'
       END AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE BETWEEN '2022-09-01' AND '2022-09-30'
ORDER BY HISTORY_ID DESC
```
