### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기)
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
`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블에서 2022년 10월 16일에 대여 중인 자동차인 경우 '대여중' 이라고 표시하고, 대여 중이지 않은 자동차인 경우 '대여 가능'을 표시하는 컬럼(컬럼명: `AVAILABILITY`)을 추가하여 자동차 ID와 `AVAILABILITY` 리스트를 출력하는 SQL문을 작성해주세요. 이때 반납 날짜가 2022년 10월 16일인 경우에도 '대여중'으로 표시해주시고 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_RENTAL_HISTORY*
|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	4|	2022-09-27|	2022-09-27|
|2|	3|	2022-10-03|	2022-10-04|
|3|	2|	2022-10-05|	2022-10-05|
|4|	1|	2022-10-11|	2022-10-16|
|5|	3|	2022-10-13|	2022-10-15|
|6|	2|	2022-10-15|	2022-10-17|

<br>

**Sample Output**

|CAR_ID|	AVAILABILITY|
|---|---|
|4|	대여 가능|
|3|	대여 가능|
|2|	대여중|
|1|	대여중|

<br>

### Solving

```sql
# 여기서 중요한 포인트는, START_DATE & END_DATE 간의 '2022-10-16' 기록이 있다면 대여 불가
# '2022-10-16' 기록이 아예 없는 것이 (=0) 대여 가능!

WITH RENTAL_AVAILABILITY AS (
    SELECT CAR_ID
         , CASE 
                WHEN '2022-10-16' BETWEEN START_DATE AND END_DATE THEN '1'
                ELSE '0'
           END AS AVAILABILITY
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
)

SELECT CAR_ID
     , CASE
            WHEN SUM(AVAILABILITY) = 1 THEN '대여중'
            ELSE '대여 가능'
        END AS AVAILABILITY
FROM RENTAL_AVAILABILITY
GROUP BY CAR_ID
ORDER BY CAR_ID DESC
```
