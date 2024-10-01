### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (과일로 만든 아이스크림 고르기)
- *table* : FIRST_HALF, ICECREAM_INFO

<br>

**FIRST_HALF**
|column|type|nullable|
|---|---|---|
|SHIPMENT_ID|	INT(N)|	FALSE|
|FLAVOR|	VARCHAR(N)|	FALSE|
|TOTAL_ORDER|	INT(N)|	FALSE|

`FIRST_HALF` 테이블 구조는 다음과 같으며, `SHIPMENT_ID`, `FLAVOR`, `TOTAL_ORDER` 는 각각 아이스크림 공장에서 아이스크림 가게까지의 출하 번호, 아이스크림 맛, 상반기 아이스크림 총주문량을 나타냅니다. `FIRST_HALF` 테이블의 기본 키는 FLAVOR입니다.

<br>

**ICECREAM_INFO**
|column|type|nullable|
|---|---|---|
|FLAVOR|	VARCHAR(N)|	FALSE|
|INGREDIENT_TYPE|	VARCHAR(N)|	FALSE|

`INGREDIENT_TYPE`에는 아이스크림의 주 성분이 설탕이면 `sugar_based`라고 입력되고, 아이스크림의 주 성분이 과일이면 `fruit_based`라고 입력됩니다. `ICECREAM_INFO`의 기본 키는 `FLAVOR`입니다. `ICECREAM_INFO`테이블의 `FLAVOR`는 `FIRST_HALF` 테이블의 `FLAVOR`의 외래 키입니다.

<br>

### Problem
상반기 아이스크림 총주문량이 3,000보다 높으면서 아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이 큰 순서대로 조회하는 SQL 문을 작성해주세요.

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
|108|	mango|	2900|
|109|	strawberry|	3100|
|110|	melon|	3150|
|111|	orange|	2900|
|112|	pineapple|	2900|

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
|mango|	fruit_based|
|strawberry|	fruit_based|
|melon|	fruit_based|
|orange|	fruit_based|
|pineapple|	fruit_based|

<br>

**Sample Output**

|FLAVOR|
|---|
|melon|
|strawberry|

<br>

### Solving

```sql
SELECT FLAVOR
FROM FIRST_HALF
WHERE TOTAL_ORDER > 3000
  AND FLAVOR IN (SELECT FLAVOR
                 FROM ICECREAM_INFO
                 WHERE INGREDIENT_TYPE = 'fruit_based')                                    
```
