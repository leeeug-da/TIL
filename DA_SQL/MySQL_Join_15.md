### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (JOIN) (특정 기간동안 대여 가능한 자동차들의 대여비용 구하기)
- *table* : CAR_RENTAL_COMPANY_CAR, CAR_RENTAL_COMPANY_RENTAL_HISTORY, CAR_RENTAL_COMPANY_DISCOUNT_PLAN

<br>

**CAR_RENTAL_COMPANY_CAR**
|column|type|
|---|---|
|CAR_ID|INTEGER|
|CAR_TYPE|VARCHAR|
|DAILY_FEE|INTEGER|
|OPTIONS|VARCHAR|

`CAR_RENTAL_COMPANY_CAR` 테이블은 아래와 같은 구조로 되어있으며, `CAR_ID`, `CAR_TYPE`, `DAILY_FEE`, `OPTIONS` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다. 자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: ''열선시트,스마트키,주차감지센서'')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

<br>

**CAR_RENTAL_COMPANY_RENTAL_HISTORY**
|column|type|
|---|---|
|HISTORY_ID|INTEGER|
|CAR_ID|INTEGER|
|START_DATE|DATE|
|END_DATE|DATE|

`CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블은 아래와 같은 구조로 되어있으며, `HISTORY_ID`, `CAR_ID`, `START_DATE`, `END_DATE` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

<br>

**CAR_RENTAL_COMPANY_DISCOUNT_PLAN**
|column|type|
|---|---|
|PLAN_ID|INTEGER|
|CAR_TYPE|VARCHAR|
|DURATION_TYPE|VARCHAR|
|DISCOUNT_RATE|INTEGER|

`CAR_RENTAL_COMPANY_DISCOUNT_PLAN` 테이블은 아래와 같은 구조로 되어있으며, `PLAN_ID`, `CAR_TYPE`, `DURATION_TYPE`, `DISCOUNT_RATE` 는 각각 요금 할인 정책 ID, 자동차 종류, 대여 기간 종류, 할인율(%)을 나타냅니다. 할인율이 적용되는 대여 기간 종류로는 '7일 이상' (대여 기간이 7일 이상 30일 미만인 경우), '30일 이상' (대여 기간이 30일 이상 90일 미만인 경우), '90일 이상' (대여 기간이 90일 이상인 경우) 이 있습니다. 대여 기간이 7일 미만인 경우 할인정책이 없습니다.

<br>

### Problem 
`CAR_RENTAL_COMPANY_CAR` 테이블과 `CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블과 `CAR_RENTAL_COMPANY_DISCOUNT_PLAN` 테이블에서 자동차 종류가 '세단' 또는 'SUV' 인 자동차 중 2022년 11월 1일부터 2022년 11월 30일까지 대여 가능하고 30일간의 대여 금액이 50만원 이상 200만원 미만인 자동차에 대해서 자동차 ID, 자동차 종류, 대여 금액(컬럼명: `FEE`) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 자동차 종류를 기준으로 오름차순 정렬, 자동차 종류까지 같은 경우 자동차 ID를 기준으로 내림차순 정렬해주세요. `FEE`의 경우 예시처럼 정수부분만 출력되어야 합니다.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_CAR*

|CAR_ID	|CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|1	|SUV	|25000	|가죽시트,열선시트,후방카메라|
|2	|세단	|14000	|스마트키,네비게이션,열선시트|
|3	|트럭	|32000	|주차감지센서,후방카메라,가죽시트|
|4	|세단	|12000	|열선시트,후방카메라|
|5	|세단	|22000	|스마트키,주차감지센서|


*CAR_RENTAL_COMPANY_RENTAL_HISTORY*

|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	1|	2022-08-27|	2022-09-02|
|2|	1|	2022-10-03|	2022-10-04|
|3|	2|	2022-10-05|	2022-10-20|
|4|	2|	2022-10-10|	2022-11-12|
|5|	3|	2022-10-16|	2022-10-17|

*CAR_RENTAL_COMPANY_DISCOUNT_PLAN*

|PLAN_ID|	CAR_TYPE|	DURATION_TYPE|	DISCOUNT_RATE|
|---|---|---|---|
|1|	트럭|	7일 이상|	5%|
|2|	트럭|	30일 이상|	7%|
|3|	트럭|	90일 이상|	10%|
|4|	세단|	7일 이상|	5%|
|5|	세단|	30일 이상|	10%|
|6|	세단|	90일 이상|	15%|
|7|	SUV|	7일 이상|	3%|
|8|	SUV|	30일 이상|	8%|
|9|	SUV|	90일 이상|	12%|

<br>

**Sample Output**

|CAR_ID|	CAR_TYPE|	FEE|
|---|---|---|
|5|	세단|	690000|
|1|	SUV|	621000|

<br>

### Solving

```sql
-- CC.CAR_ID = CR.CAR_ID
-- CC.CAR_TYPE = CD.CAR_TYPE

-- CC.CAR_ID
-- CC.CAR_TYPE = '세단' or 'SUV'
-- CR.END_DATE 대여 가능 = NOT BETWEEN '2022-11-01' AND '2022-11-30'
--  30일간의 대여 금액 = BETWEEN 500000 AND 2000000
     
SELECT CC.CAR_ID
     , CC.CAR_TYPE
     , FLOOR(CC.DAILY_FEE*30*(1-CD.DISCOUNT_RATE*0.01)) AS FEE
FROM CAR_RENTAL_COMPANY_CAR CC
 JOIN CAR_RENTAL_COMPANY_RENTAL_HISTORY CR ON CC.CAR_ID = CR.CAR_ID
 JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN CD ON CC.CAR_TYPE = CD.CAR_TYPE
WHERE CC.CAR_TYPE IN ('세단', 'SUV')
AND CD.DURATION_TYPE = '30일 이상'
GROUP BY CC.CAR_ID
HAVING MAX(CR.END_DATE) < '2022-11-01'
   AND FEE >= 500000 AND FEE < 2000000
ORDER BY FEE DESC, CC.CAR_TYPE, CAR_ID DESC
```
