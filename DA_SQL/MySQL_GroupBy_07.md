### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (식품분류별 가장 비싼 식품의 정보 조회하기)
- *table* : FOOD_PRODUCT

<br>

**FOOD_PRODUCT**
|column|type|nullable|
|---|---|---|
|PRODUCT_ID|	VARCHAR(10)|	FALSE|
|PRODUCT_NAME|	VARCHAR(50)|	FALSE|
|PRODUCT_CD|	VARCHAR(10)|	TRUE|
|CATEGORY|	VARCHAR(10)|	TRUE|
|PRICE|	NUMBER|	TRUE|

`FOOD_PRODUCT` 테이블은 다음과 같으며 `PRODUCT_ID`, `PRODUCT_NAME`, `PRODUCT_CD`, `CATEGORY`, `PRICE`는 식품 ID, 식품 이름, 식품코드, 식품분류, 식품 가격을 의미합니다.

<br>

### Problem 
`FOOD_PRODUCT` 테이블에서 식품분류별로 가격이 제일 비싼 식품의 분류, 가격, 이름을 조회하는 SQL문을 작성해주세요. 이때 식품분류가 '과자', '국', '김치', '식용유'인 경우만 출력시켜 주시고 결과는 식품 가격을 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*FOOD_PRODUCT*
|PRODUCT_ID|	PRODUCT_NAME|	PRODUCT_CD|	CATEGORY|	PRICE|
|---|---|---|---|---|
|P0018|	맛있는고추기름|	CD_OL00008|	식용유|	6100|
|P0019|	맛있는카놀라유|	CD_OL00009|	식용유|	5100|
|P0020|	맛있는산초유|	CD_OL00010|	식용유|	6500|
|P0021|	맛있는케첩|	CD_SC00001|	소스|	4500|
|P0022|	맛있는마요네즈|	CD_SC00002|	소스|	4700|
|P0039|	맛있는황도|	CD_CN00008|	캔|	4100|
|P0040|	맛있는명이나물|	CD_CN00009|	캔|	3500|
|P0041|	맛있는보리차|	CD_TE00010|	차|	3400|
|P0042|	맛있는메밀차|	CD_TE00001|	차|	3500|
|P0099|	맛있는맛동산|	CD_CK00002|	과자|	1800|

<br>

**Sample Output**

|CATEGORY|	MAX_PRICE|	PRODUCT_NAME|
|---|---|---|
|식용유|	6500|	맛있는산초유|
|과자|	1800|	맛있는맛동산|

<br>

### Solving

```sql
WITH MAX_PRICE AS (
    SELECT CATEGORY, MAX(PRICE) AS MAX_PRICE
    FROM FOOD_PRODUCT
    GROUP BY CATEGORY
    HAVING CATEGORY IN ('과자', '국', '김치', '식용유')
)
SELECT FP.CATEGORY
     , MP.MAX_PRICE
     , FP.PRODUCT_NAME
FROM FOOD_PRODUCT FP
 JOIN MAX_PRICE MP ON FP.CATEGORY = MP.CATEGORY
                  AND FP.PRICE = MP.MAX_PRICE
ORDER BY MAX_PRICE DESC
```
