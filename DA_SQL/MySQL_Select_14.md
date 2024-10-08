### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (강원도에 위치한 생산공장 목록 출력하기)
- *table* : FOOD_FACTORY

<br>

**FOOD_FACTORY**
|column|type|nullable|
|---|---|---|
|FACTORY_ID|	VARCHAR(10)|	FALSE|
|FACTORY_NAME|	VARCHAR(50)|	FALSE|
|ADDRESS|	VARCHAR(100)|	FALSE|
|TLNO|	VARCHAR(20)|	TRUE|

`FOOD_FACTORY` 테이블은 다음과 같으며 `FACTORY_ID`, `FACTORY_NAME`, `ADDRESS`, `TLNO`는 각각 공장 ID, 공장 이름, 주소, 전화번호를 의미합니다.

<br>

### Problem
`FOOD_FACTORY` 테이블에서 강원도에 위치한 식품공장의 공장 ID, 공장 이름, 주소를 조회하는 SQL문을 작성해주세요. 이때 결과는 공장 ID를 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*FOOD_FACTORY*
|FACTORY_ID|	FACTORY_NAME|	ADDRESS|	TLNO|
|---|---|---|---|
|FT19980003|	(주)맛있는라면|	강원도 정선군 남면 칠현로 679|	033-431-3122|
|FT19980004|	(주)맛있는기름|	경기도 평택시 포승읍 포승공단순환로 245|	031-651-2410|
|FT20010001|	(주)맛있는소스|	경상북도 구미시 1공단로7길 58-11|	054-231-2121|
|FT20010002|	(주)맛있는통조림|	전라남도 영암군 미암면 곤미현로 1336|	061-341-5210|
|FT20100001|	(주)맛있는차|	전라남도 장성군 서삼면 장산리 233-1번지|	061-661-1420|

<br>

**Sample Output**

|FACTORY_ID|	FACTORY_NAME|	ADDRESS|
|---|---|---|
|FT19980003|	(주)맛있는라면|	강원도 정선군 남면 칠현로 679|
|FT20100003|	(주)맛있는음료|	강원도 원주시 문막읍 문막공단길 154|
|FT20100004|	(주)맛있는국|	강원도 평창군 봉평면 진조길 227-35|

<br>

### Solving

```sql
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
FROM FOOD_FACTORY
WHERE ADDRESS LIKE '강원도%'
ORDER BY FACTORY_ID                          
```
