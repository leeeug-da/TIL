### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (대여 기록이 존재하는 자동차 리스트 구하기)
- *table* : CAR_RENTAL_COMPANY_CAR, CAR_RENTAL_COMPANY_RENTAL_HISTORY

<br>

**CAR_RENTAL_COMPANY_CAR**
|column|type|nullable|
|---|---|---|
|CAR_ID|	INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE|	INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

`CAR_RENTAL_COMPANY_CAR` 테이블은 아래와 같은 구조로 되어있으며, `CAR_ID`, `CAR_TYPE`, `DAILY_FEE`, `OPTIONS` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

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
`CAR_RENTAL_COMPANY_CAR` 테이블과 `CAR_RENTAL_COMPANY_RENTAL_HISTORY` 테이블에서 자동차 종류가 '세단'인 자동차들 중 10월에 대여를 시작한 기록이 있는 자동차 ID 리스트를 출력하는 SQL문을 작성해주세요. 자동차 ID 리스트는 중복이 없어야 하며, 자동차 ID를 기준으로 내림차순 정렬해주세요.



<br>

**Sample Input**

*CAR_RENTAL_COMPANY_CAR*
|CAR_ID|	CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|1|	세단|	16000|	가죽시트,열선시트,후방카메라|
|2|	SUV|	14000|	스마트키,네비게이션,열선시트|
|3|	세단|	22000|	주차감지센서,후방카메라,가죽시트|
|4|	세단|	12000|	주차감지센서|
  
<br>

*CAR_RENTAL_COMPANY_RENTAL_HISTORY*
|HISTORY_ID|	CAR_ID|	START_DATE|	END_DATE|
|---|---|---|---|
|1|	4|	2022-09-27|	2022-09-27|
|2|	3|	2022-10-03|	2022-10-04|
|3|	2|	2022-10-05|	2022-10-05|
|4|	1|	2022-10-11|	2022-10-14|
|5|	3|	2022-10-13|	2022-10-15|

<br>

**Sample Output**

|CAR_ID|
|---|
|3|
|1|

<br>

### Solving

```sql
SELECT DISTINCT(CAR_ID) AS CAR_ID
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE BETWEEN '2022-10-01' AND '2022-10-31'
  AND CAR_ID IN (SELECT CAR_ID
                 FROM CAR_RENTAL_COMPANY_CAR
                 WHERE CAR_TYPE = '세단'
                )
ORDER BY CAR_ID DESC
```
