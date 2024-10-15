### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (오프라인/온라인 판매 데이터 통합하기)
- *table* : ONLINE_SALE, OFFLINE_SALE

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

**OFFLINE_SALE**
|column|type|nullable|
|---|---|---|
|OFFLINE_SALE_ID|	INTEGER|	FALSE|
|PRODUCT_ID|	INTEGER|	FALSE|
|SALES_AMOUNT|	INTEGER|	FALSE|
|SALES_DATE|	DATE|	FALSE|

`OFFLINE_SALE` 테이블은 아래와 같은 구조로 되어있으며 `OFFLINE_SALE_ID`, `PRODUCT_ID`, `SALES_AMOUNT`, `SALES_DATE`는 각각 오프라인 상품 판매 ID, 상품 ID, 판매량, 판매일을 나타냅니다.

<br>

### Problem
`ONLINE_SALE` 테이블과 `OFFLINE_SALE` 테이블에서 2022년 3월의 오프라인/온라인 상품 판매 데이터의 판매 날짜, 상품ID, 유저ID, 판매량을 출력하는 SQL문을 작성해주세요. `OFFLINE_SALE` 테이블의 판매 데이터의 `USER_ID` 값은 NULL 로 표시해주세요. 결과는 판매일을 기준으로 오름차순 정렬해주시고 판매일이 같다면 상품 ID를 기준으로 오름차순, 상품ID까지 같다면 유저 ID를 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*ONLINE_SALE*
|ONLINE_SALE_ID|	USER_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|---|
|1|	1|	3|	2|	2022-02-25|
|2|	4|	4|	1|	2022-03-01|
|4|	2|	2|	2|	2022-03-02|
|3|	6|	3|	3|	2022-03-02|
|5|	5|	5|	1|	2022-03-03|
|6|	5|	7|	1|	2022-04-06|

<br>

*OFFLINE_SALE*
|OFFLINE_SALE_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|
|1|	1|	2|	2022-02-21|
|4|	1|	2|	2022-03-01|
|3|	3|	3|	2022-03-01|
|2|	4|	1|	2022-03-01|
|5|	2|	1|	2022-03-03|
|6|	2|	1|	2022-04-01|

<br>

**Sample Output**
|SALES_DATE|	PRODUCT_ID|	USER_ID|	SALES_AMOUNT|
|---|---|---|---|
|2022-03-01|	1|	NULL|	2|
|2022-03-01|	3|	NULL|	3|
|2022-03-01|	4|	NULL|	1|
|2022-03-01|	4|	4|	1|
|2022-03-02|	2|	2|	2|
|2022-03-02|	3|	6|	3|
|2022-03-03|	2|	NULL|	1|
|2022-03-03|	5|	5|	1|


<br>

### Solving

```sql
SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') AS SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
FROM (SELECT SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
      FROM ONLINE_SALE
      UNION ALL
      SELECT SALES_DATE, PRODUCT_ID, NULL AS USER_ID, SALES_AMOUNT 
      FROM OFFLINE_SALE
     ) A
WHERE DATE_FORMAT(SALES_DATE, '%Y-%m') = '2022-03'
ORDER BY SALES_DATE, PRODUCT_ID, USER_ID              
```
