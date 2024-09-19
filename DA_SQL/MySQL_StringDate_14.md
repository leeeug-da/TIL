### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (카테고리 별 상품 개수 구하기)
- *table* : PRODUCT

<br>

**PRODUCT**
|column|type|nullable|
|---|---|---|
|PRODUCT_ID|	INTEGER|	FALSE|
|PRODUCT_CODE|	VARCHAR(8)|	FALSE|
|PRICE|	INTEGER|	FALSE|

`PRODUCT` 테이블은 아래와 같은 구조로 되어있으며, `PRODUCT_ID`, `PRODUCT_CODE`, `PRICE`는 각각 상품 ID, 상품코드, 판매가를 나타냅니다. 상품 별로 중복되지 않는 8자리 상품코드 값을 가지며, 앞 2자리는 카테고리 코드를 의미합니다.

<br>

### Problem
`PRODUCT` 테이블에서 상품 카테고리 코드(`PRODUCT_CODE` 앞 2자리) 별 상품 개수를 출력하는 SQL문을 작성해주세요. 결과는 상품 카테고리 코드를 기준으로 오름차순 정렬해주세요.



<br>

**Sample Input**

*PRODUCT*
|PRODUCT_ID|	PRODUCT_CODE|	PRICE|
|---|---|---|
|1|	A1000011|	10000|
|2|	A1000045|	9000|
|3|	C3000002|	22000|
|4|	C3000006|	15000|
5|	C3000010|	30000|
|6|	K1000023|	17000|
  
<br>

**Sample Output**

|CATEGORY|	PRODUCTS|
|---|---|
|A1|	2|
|C3|	3|
|K1|	1|


<br>

### Solving

```sql
SELECT SUBSTR(PRODUCT_CODE, 1, 2) AS CATEGORY
     , COUNT(DISTINCT PRODUCT_ID) AS PRODUCTS
FROM PRODUCT
GROUP BY CATEGORY
ORDER BY CATEGORY
```
