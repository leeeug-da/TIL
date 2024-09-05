### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (특정 옵션이 포함된 자동차 리스트 구하기)
- *table* : CAR_RENTAL_COMPANY_CAR

<br>

**CAR_RENTAL_COMPANY_CAR**
|column|type|nullable|
|---|---|---|
|CAR_ID|	INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE|	INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

`CAR_RENTAL_COMPANY_CAR` 테이블은 아래와 같은 구조로 되어있으며, `CAR_ID`, `CAR_TYPE`, `DAILY_FEE`, `OPTIONS` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(옵션 리스트 값 예시: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

<br>

### Problem
`CAR_RENTAL_COMPANY_CAR` 테이블에서 '네비게이션' 옵션이 포함된 자동차 리스트를 출력하는 SQL문을 작성해주세요. 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_CAR*
|CAR_ID|	CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|1|	세단|	16000|	가죽시트,열선시트,후방카메라|
|2|	SUV|	14000|	스마트키,네비게이션,열선시트|
|3|	SUV|	22000|	주차감지센서,후방카메라,네비게이션|
  
<br>

**Sample Output**

|CAR_ID|	CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|3|	SUV|	22000|	주차감지센서,후방카메라,네비게이션|
|2|	SUV|	14000|	스마트키,네비게이션,열선시트|

<br>

### Solving

```sql
SELECT *
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%네비게이션%'
ORDER BY CAR_ID DESC
```
