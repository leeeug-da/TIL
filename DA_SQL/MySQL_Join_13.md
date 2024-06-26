### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (JOIN) (상품 별 오프라인 매출 구하기)
- *table* : PRODUCT, OFFLINE_SALE

<br>

**PRODUCT**
|column|type|
|---|---|
|PRODUCT_ID|INTEGER|
|PRODUCT_CODE|VARCHAR|
|PRICE|INTEGER|

PRODUCT 테이블은 아래와 같은 구조로 PRODUCT_ID, PRODUCT_CODE, PRICE는 각각 상품 ID, 상품코드, 판매가를 나타냅니다.

**OFFLINE_SALE**
|column|type|
|---|---|
|OFFLINE_SALE_ID|INTEGER|
|PRODUCT_ID|INTEGER|
|SALES_AMOUNT|INTEGER|
|SALES_DATE|DATE|

OFFLINE_SALE 테이블은 아래와 같은 구조로 되어있으며 OFFLINE_SALE_ID, PRODUCT_ID, SALES_AMOUNT, SALES_DATE는 각각 오프라인 상품 판매 ID, 상품 ID, 판매량, 판매일을 나타냅니다. 동일한 날짜, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.

<br>

### Problem 
PRODUCT 테이블과 OFFLINE_SALE 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성해주세요. 결과는 매출액을 기준으로 내림차순 정렬해주시고 매출액이 같다면 상품코드를 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*PRODUCT*
|PRODUCT_ID|	PRODUCT_CODE|	PRICE|
|---|---|---
|1	|A1000011|	15000|
|2	|A1000045|	8000|
|3	|C3000002|	42000|


*OFFLINE_SALE*
|OFFLINE_SALE_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|
|1	|1	|2	|2022-02-21|
|2	|1	|2	|2022-03-02|
|3	|3	|3	|2022-05-01|
|4	|2	|1	|2022-05-24|
|5	|1	|2	|2022-07-14|
|6	|2	|1	|2022-09-22|

**Sample Output**

|PRODUCT_CODE|	SALES|
|---|---|
|C3000002|	126000|
|A1000011|	90000|
|A1000045|	16000|

<br>

### Solving

```sql
-- 상품코드 별 매출액 합계 SUM(P.PRICE * O.SALES_AMOUNT)
-- SALES DESC, PRODUCT_CODE 

SELECT PRODUCT_CODE
     , SUM(P.PRICE * O.SALES_AMOUNT) AS SALES
FROM PRODUCT P
 JOIN OFFLINE_SALE O USING (PRODUCT_ID)
GROUP BY PRODUCT_CODE
ORDER BY SALES DESC, PRODUCT_CODE
```
