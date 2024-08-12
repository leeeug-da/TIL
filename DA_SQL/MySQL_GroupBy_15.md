### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
가격대 별 상품 개수 구하기)
- *table* : PRODUCT

<br>

**PRODUCTS**
|column|type|nullable|
|---|---|---|
|PRODUCT_ID|	INTEGER|	FALSE|
|PRODUCT_CODE|	VARCHAR(8)|	FALSE|
|PRICE|	INTEGER|	FALSE|


`PRODUCT` 테이블은 아래와 같은 구조로 되어있으며, `PRODUCT_ID`, `PRODUCT_CODE`, `PRICE`는 각각 상품 ID, 상품코드, 판매가를 나타냅니다. 상품 별로 중복되지 않는 8자리 상품코드 값을 가지며 앞 2자리는 카테고리 코드를 나타냅니다.

<br>

### Problem
`PRODUCT` 테이블에서 만원 단위의 가격대 별로 상품 개수를 출력하는 SQL 문을 작성해주세요. 이때 컬럼명은 각각 컬럼명은 PRICE_GROUP, PRODUCTS로 지정해주시고 가격대 정보는 각 구간의 최소금액(10,000원 이상 ~ 20,000 미만인 구간인 경우 10,000)으로 표시해주세요. 결과는 가격대를 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**
*PRODUCT*
|PRODUCT_ID|	PRODUCT_CODE|	PRICE|
|---|---|---|
|1|	A1000011|	10000|
|2|	A1000045|	9000|
|3|	C3000002|	22000|
|4|	C3000006|	15000|
|5|	C3000010|	30000|
|6|	K1000023|	17000|

<br>

**Sample Output**

|PRICE_GROUP|	PRODUCTS|
|---|---|
|0|	1|
|10000|	3|
|20000|	1|
|30000|	1|

<br>

### Solving

```sql
SELECT CASE 
            WHEN PRICE < 10000 THEN 0
            WHEN PRICE < 20000 THEN 10000
            WHEN PRICE < 30000 THEN 20000
            WHEN PRICE < 40000 THEN 30000
            WHEN PRICE < 50000 THEN 40000
            WHEN PRICE < 60000 THEN 50000
            WHEN PRICE < 70000 THEN 60000
            WHEN PRICE < 80000 THEN 70000
            WHEN PRICE < 90000 THEN 80000
        END AS 'PRICE_GROUP'
    , COUNT(DISTINCT PRODUCT_CODE) AS PRODUCTS
FROM PRODUCT
GROUP BY PRICE_GROUP
ORDER BY PRICE_GROUP
```
