### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (자동차 대여 기록 별 대여 금액 구하기)
- *table* : CAR_RENTAL_COMPANY_CAR, CAR_RENTAL_COMPANY_RENTAL_HISTORY, CAR_RENTAL_COMPANY_DISCOUNT_PLAN

<br>

**CAR_RENTAL_COMPANY_CAR**
|column|type|nullable|
|---|---|---|
|CAR_ID|	INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE|	INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

`CAR_RENTAL_COMPANY_CAR` 테이블은 아래와 같은 구조로 되어있으며, `CAR_ID`, `CAR_TYPE`, `DAILY_FEE`, `OPTIONS` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

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

**CAR_RENTAL_COMPANY_DISCOUNT_PLAN**
|column|type|nullable|
|---|---|---|
|PLAN_ID|	INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DURATION_TYPE|	VARCHAR(255)|	FALSE|
|DISCOUNT_RATE|	INTEGER|	FALSE|

`CAR_RENTAL_COMPANY_DISCOUNT_PLAN` 테이블은 아래와 같은 구조로 되어있으며, `PLAN_ID`, `CAR_TYPE`, `DURATION_TYPE`, `DISCOUNT_RATE` 는 각각 요금 할인 정책 ID, 자동차 종류, 대여 기간 종류, 할인율(%)을 나타냅니다.

할인율이 적용되는 대여 기간 종류로는 '7일 이상' (대여 기간이 7일 이상 30일 미만인 경우), '30일 이상' (대여 기간이 30일 이상 90일 미만인 경우), '90일 이상' (대여 기간이 90일 이상인 경우) 이 있습니다. 대여 기간이 7일 미만인 경우 할인정책이 없습니다.

<br>

### Problem
`CAR_RENTAL_COMPANY_CAR` 테이블과 `CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블과 `CAR_RENTAL_COMPANY_DISCOUNT_PLAN` 테이블에서 자동차 종류가 '트럭'인 자동차의 대여 기록에 대해서 대여 기록 별로 대여 금액(컬럼명: FEE)을 구하여 대여 기록 ID와 대여 금액 리스트를 출력하는 SQL문을 작성해주세요. 결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 대여 기록 ID를 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_CAR*
|CAR_ID|	CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|1|	트럭|	26000|	가죽시트,열선시트,후방카메라|
|2|	SUV|	14000|	스마트키,네비게이션,열선시트|
|3|	트럭|	32000|	주차감지센서,후방카메라,가죽시트|
  
<br>

*CAR_RENTAL_COMPANY_RENTAL_HISTORY*
|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	1|	2022-07-27|	2022-08-02|
|2	|1|	2022-08-03|	2022-08-04|
|3	|2|	2022-08-05|	2022-08-05|
|4	|2|	2022-08-09|	2022-08-12|
|5	|3|	2022-09-16|	2022-10-15|

<br>

*CAR_RENTAL_COMPANY_DISCOUNT_PLAN*
|PLAN_ID|	CAR_TYPE|	DURATION_TYPE|	DISCOUNT_RATE|
|---|---|---|---|
|1|	트럭|	7일 이상|	5%|
|2|	트럭|	30일 이상|	7%|
|3|	트럭|	90일 이상|	10%|
|4|	세단|	7일 이상|	5%|
|5|	세단|	30일 이상|	10%|
|6|	세단|	90일 이상|	15%|

<br>

자동차 종류가 '트럭' 인 자동차의 대여 기록에 대해서 대여 기간을 구하면,

대여 기록 ID가 1인 경우, 7일
대여 기록 ID가 2인 경우, 2일
대여 기록 ID가 5인 경우, 30일입니다.
대여 기간 별로 일일 대여 요금에 알맞은 할인율을 곱하여 금액을 구하면 다음과 같습니다.

대여 기록 ID가 1인 경우, 일일 대여 금액 26,000원에서 5% 할인율을 적용하고 7일을 곱하면 총 대여 금액은 172,900원
대여 기록 ID가 2인 경우, 일일 대여 금액 26,000원에 2일을 곱하면 총 대여 금액은 52,000원
대여 기록 ID가 5인 경우, 일일 대여 금액 32,000원에서 7% 할인율을 적용하고 30일을 곱하면 총 대여 금액은 892,800원이 되므로, 대여 금액을 기준으로 내림차순 정렬 및 대여 기록 ID를 기준으로 내림차순 정렬하면 다음과 같아야 합니다.

<br>

**Sample Output**

|HISTORY_ID|	FEE|
|---|---|
|5|	892800|
|1|	172900|
|2|	52000|

<br>

### Solving

```sql
-- 자동차 종류가 '트럭'인
-- 대여 기록 별로 대여 금액(컬럼명: FEE)을 구하여 대여 기록 ID와 대여 금액 리스트를 출력
-- 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 대여 기록 ID를 기준으로 내림차순 정렬
-- 대여 기록 ID가 1인 경우, 일일 대여 금액 26,000원에서 5% 할인율을 적용하고 7일을 곱하면 총 대여 금액은 172,900원

SELECT A.HISTORY_ID
     , (TIMESTAMPDIFF(DAY, A.START_DATE, A.END_DATE)+1) * 
       (B.DAILY_FEE - (B.DAILY_FEE/100 * REPLACE(IFNULL(C.DISCOUNT_RATE,0), '%', ''))) AS FEE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY A
 INNER JOIN CAR_RENTAL_COMPANY_CAR B 
         ON B.CAR_ID = A.CAR_ID 
         AND B.CAR_TYPE = '트럭'
 LEFT JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN C 
        ON C.CAR_TYPE = B.CAR_TYPE
       AND C.DURATION_TYPE = CASE WHEN (TIMESTAMPDIFF(DAY, A.START_DATE, A.END_DATE) + 1) >= 90 THEN '90일 이상'
                                  WHEN (TIMESTAMPDIFF(DAY, A.START_DATE, A.END_DATE) + 1) >= 30 THEN '30일 이상'
                                  WHEN (TIMESTAMPDIFF(DAY, A.START_DATE, A.END_DATE) + 1) >= 7 THEN '7일 이상'
                              END 
ORDER BY FEE DESC, A.HISTORY_ID DESC                                        
```
