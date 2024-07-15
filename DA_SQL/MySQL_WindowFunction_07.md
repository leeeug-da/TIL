### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql 
- *table* : records (US E-Commerce Records 2020)

**records**
|column|type|
|---|---|
|order_date|date|
|order_id|string|
|ship_mode|string|
|customer_id|string|
|segment|string|
|country|string|
|city|string|
|state|string|
|postal_code|integer|
|region|string|
|product_id|string|
|category|string|
|sub_category|string|
|product_name|string|
|sales|number|
|quantity|integer|
|discount|number|
|profit|number|


<br>

### Problem 
서브 카테고리별 매출액(`sales`)을 계산하고 그 매출액이 각 서브 카테고리가 속해있는 카테고리 안에서 비중을 얼마나 차지하는지, 그리고 전체 매출액에서 비중을 얼마나 차지하는지 각각 계산해 주세요. 결과물은 아래 모양을 참고하세요.

결과에 포함되어야 하는 컬럼

- `category`: 카테고리 이름
- `sub_category`: 서브 카테고리 이름
- `sales_sub_category`: 서브 카테고리별 매출액 합계
- `sales_category`: 카테고리별 매출액 합계
- `sales_total`: 전체 매출액
- `pct_in_category`: 카테고리 매출 중 해당 서브 카테고리의 매출 비율
- `pct_in_total`: 전체 매출 중 해당 서브 카테고리의 매출 비율


### Solving
```sql
WITH sales AS (
  SELECT category
      , sub_category
      , SUM(sales) AS sales_sub_category
  FROM records
  GROUP BY category, sub_category
)

SELECT *
     , SUM(sales_sub_category) OVER (PARTITION BY category) AS sales_category
     , SUM(sales_sub_category) OVER () AS sales_total
     , sales_sub_category / SUM(sales_sub_category) OVER (PARTITION BY category) AS pct_in_category
     , sales_sub_category / SUM(sales_sub_category) OVER () AS pct_in_total
FROM sales
```
