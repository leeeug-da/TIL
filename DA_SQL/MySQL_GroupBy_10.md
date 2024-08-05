### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (성분으로 구분한 아이스크림 총 주문량)
- *table* : FIRST_HALF, ICECREAM_INFO

<br>

**FIRST_HALF**
|column|type|nullable|
|---|---|---|
|SHIPMENT_ID|	INT(N)|	FALSE|
|FLAVOR|	VARCHAR(N)|	FALSE|
|TOTAL_ORDER|	INT(N)|	FALSE|

`FIRST_HALF` 테이블 구조는 다음과 같으며, `SHIPMENT_ID`, `FLAVOR`, `TOTAL_ORDER` 는 각각 아이스크림 공장에서 아이스크림 가게까지의 출하 번호, 아이스크림 맛, 상반기 아이스크림 총주문량을 나타냅니다. `FIRST_HALF` 테이블의 기본 키는 `FLAVOR`입니다.

<br>

**ICECREAM_INFO**
|column|type|nullable|
|---|---|---|
|FLAVOR|	VARCHAR(N)|	FALSE|
|INGREDIENT_TYPE|	VARCHAR(N)|	FALSE|

`ICECREAM_INFO` 테이블 구조는 다음과 같으며, `FLAVOR`, `INGREDITENT_TYPE` 은 각각 아이스크림 맛, 아이스크림의 성분 타입을 나타냅니다. `INGREDIENT_TYPE`에는 아이스크림의 주 성분이 설탕이면 `sugar_based`라고 입력되고, 아이스크림의 주 성분이 과일이면 `fruit_based`라고 입력됩니다. `ICECREAM_INFO`의 기본 키는 `FLAVOR`입니다. `ICECREAM_INFO`테이블의 `FLAVOR`는 `FIRST_HALF` 테이블의 `FLAVOR`의 외래 키입니다.

### Problem 
상반기 동안 각 아이스크림 성분 타입과 성분 타입에 대한 아이스크림의 총주문량을 총주문량이 작은 순서대로 조회하는 SQL 문을 작성해주세요. 이때 총주문량을 나타내는 컬럼명은 TOTAL_ORDER로 지정해주세요.

<br>

**Sample Input**

*FIRST_HALF*
|SHIPMENT_ID|	FLAVOR|	TOTAL_ORDER|
|---|---|---|
|101|	chocolate|	3200|
|102|	vanilla|	2800|
|103|	mint_chocolate|	1700|
|104|	caramel|	2600|
|105|	white_chocolate|	3100|
|106|	peach|	2450|
|107|	watermelon|	2150|

<br>

*ICECREAM_INFO*
|FLAVOR|	INGREDIENT_TYPE|
|---|---|
|chocolate|	sugar_based|
|vanilla|	sugar_based|
|mint_chocolate|	sugar_based|
|caramel|	sugar_based|
|white_chocolate|	sugar_based|
|peach|	fruit_based|
|watermelon|	fruit_based|

<br>

**Sample Output**

|INGREDIENT_TYPE|	TOTAL_ORDER|
|---|---|
|sugar_based|	13400|
|fruit_based|	19550|

<br>

### Solving

```sql
SELECT I.INGREDIENT_TYPE
     , SUM(F.TOTAL_ORDER) AS TOTAL_ORDER
FROM FIRST_HALF F
 JOIN ICECREAM_INFO I ON F.FLAVOR = I.FLAVOR
GROUP BY I.INGREDIENT_TYPE
ORDER BY TOTAL_ORDER 
```
