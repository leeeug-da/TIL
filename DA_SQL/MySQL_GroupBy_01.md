### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기)
- *table* : CAR_RENTAL_COMPANY_CAR

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

### Problem 
`CAR_RENTAL_COMPANY_CAR` 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성해주세요. 이때 자동차 수에 대한 컬럼명은 `CARS`로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*CAR_RENTAL_COMPANY_CAR*

|CAR_ID	|CAR_TYPE|	DAILY_FEE|	OPTIONS|
|---|---|---|---|
|1	|세단	|16000	|가죽시트,열선시트,후방카메라|
|2	|SUV	|14000	|스마트키,네비게이션,열선시트|
|3	|SUV	|22000	|주차감지센서,후방카메라,가죽시트|
|4	|트럭	|35000	|주차감지센서,네비게이션,열선시트|
|5	|SUV	|16000	|가죽시트,네비게이션,열선시트,후방카메라,주차감지센서|

<br>

**Sample Output**

|CAR_TYPE|CARS|
|---|---|
|SUV|2|
|세단|1|
|트럭|1|

<br>

### Solving

```sql
SELECT CAR_TYPE
     , COUNT(DISTINCT CAR_ID) AS CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%통풍시트%' OR
      OPTIONS LIKE '%열선시트%' OR
      OPTIONS LIKE '%가죽시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
```
