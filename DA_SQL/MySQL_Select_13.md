### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (인기있는 아이스크림)
- *table* : FIRST_HALF

<br>

**FIRST_HALF**
|column|type|nullable|
|---|---|---|
|SHIPMENT_ID|	INT(N)|	FALSE|
|FLAVOR|	VARCHAR(N)|	FALSE|
|TOTAL_ORDER|	INT(N)|	FALSE|

`FIRST_HALF` 테이블 구조는 다음과 같으며, `SHIPMENT_ID`, `FLAVOR`, `TOTAL_ORDER는` 각각 아이스크림 공장에서 아이스크림 가게까지의 출하 번호, 아이스크림 맛, 상반기 아이스크림 총주문량을 나타냅니다.

<br>

### Problem
상반기에 판매된 아이스크림의 맛을 총주문량을 기준으로 내림차순 정렬하고 총주문량이 같다면 출하 번호를 기준으로 오름차순 정렬하여 조회하는 SQL 문을 작성해주세요.

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

**Sample Output**

|FLAVOR|
|---|
|chocolate|
|melon|
|white_chocolate|
|strawberry|
|mango|
|orange|
|pineapple|
|vanilla|
|caramel|
|peach|
|watermelon|
|mint_chocolate|

<br>

### Solving

```sql
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID                           
```
