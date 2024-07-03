### Topic
- Aggregation
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SUM, MAX, MIN) (가격이 제일 비싼 식품의 정보 출력하기)
- *table* : FOOD_PRODUCT

**FOOD_PRODUCT**
|column|type|
|---|---|
|PRODUCT_ID|VARCHAR|
|PRODUCT_NAME|VARCHAR|
|PRODUCT_CD|VARCHAR|
|CATEGORY|VARCHAR|
|PRICE|NUMBER|

`FOOD_PRODUCT` 테이블은 다음과 같으며 `PRODUCT_ID`, `PRODUCT_NAME`, `PRODUCT_CD`, `CATEGORY`, `PRICE`는 식품 ID, 식품 이름, 식품 코드, 식품분류, 식품 가격을 의미합니다.



### Problem 
`FOOD_PRODUCT` 테이블에서 가격이 제일 비싼 식품의 식품 ID, 식품 이름, 식품 코드, 식품분류, 식품 가격을 조회하는 SQL문을 작성해주세요.

**Sample Input**

*FOOD_PRODUCT*
|PRODUCT_ID|	PRODUCT_NAME|	PRODUCT_CD|	CATEGORY|	PRICE|
|---|---|---|---|---|
|P0018|	맛있는고추기름|	CD_OL00008|	식용유|	6100|
|P0019|	맛있는카놀라유|	CD_OL00009|	식용유|	5100|
|P0020|	맛있는산초유|	CD_OL00010|	식용유|	6500|
|P0021|	맛있는케첩|	CD_OL00001|	소스|	4500|
|P0022|	맛있는마요네즈|	CD_OL00002|	소스|	4700|

**Sample Output**
|PRODUCT_ID|	PRODUCT_NAME|	PRODUCT_CD|	CATEGORY|	PRICE|
|---|---|---|---|---|
|P0020|	맛있는산초유|	CD_OL00010|	식용유|	6500|


### Solving

```sql
SELECT *
FROM FOOD_PRODUCT
ORDER BY PRICE DESC
LIMIT 1;
```

