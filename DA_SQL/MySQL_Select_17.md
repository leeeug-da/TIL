### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (재구매가 일어난 상품과 회원 리스트 구하기)
- *table* : ONLINE_SALE 

<br>

**ONLINE_SALE**
|column|type|nullable|
|---|---|---|
|ONLINE_SALE_ID|	INTEGER|	FALSE|
|USER_ID|	INTEGER|	FALSE|
|PRODUCT_ID|	INTEGER|	FALSE|
|SALES_AMOUNT|	INTEGER|	FALSE|
|SALES_DATE|	DATE|	FALSE|

`ONLINE_SALE` 테이블은 아래와 같은 구조로 되어있으며 `ONLINE_SALE_ID`, `USER_ID`, `PRODUCT_ID`, `SALES_AMOUNT`, `SALES_DATE`는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.

<br>

### Problem
`ONLINE_SALE` 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.
<br>

**Sample Input**

*ONLINE_SALE*
|ONLINE_SALE_ID|	USER_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|---|
|1|	1|	3|	2|	2022-02-25|
|2|	1|	4|	1|	2022-03-01|
|4|	2|	4|	2|	2022-03-12|
|3|	1|	3|	3|	2022-03-31|
|5|	3|	5|	1|	2022-04-03|
|6|	2|	4|	1|	2022-04-06|
|2|	1|	4|	2|	2022-05-11|

<br>

**Sample Output**

|USER_ID|	PRODUCT_ID|
|---|---|
|1|	4|
|1|	3|
|2|	4|

<br>

### Solving

```sql
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(ONLINE_SALE_ID) > 1
ORDER BY USER_ID, PRODUCT_ID DESC                    
```
