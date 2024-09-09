### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (조건별로 분류하여 주문상태 출력하기)
- *table* : FOOD_ORDER

<br>

**FOOD_ORDER**
|column|type|nullable|
|---|---|---|
|ORDER_ID|	VARCHAR(10)|	FALSE|
|PRODUCT_ID|	VARCHAR(5)|	FALSE|
|AMOUNT|	NUMBER|	FALSE|
|PRODUCE_DATE|	DATE|	TRUE|
|IN_DATE|	DATE|	TRUE|
|OUT_DATE|	DATE|	TRUE|
|FACTORY_ID|	VARCHAR(10)|	FALSE|
|WAREHOUSE_ID|	VARCHAR(10)|	FALSE|

<br>

### Problem
`FOOD_ORDER` 테이블에서 2022년 5월 1일을 기준으로 주문 ID, 제품 ID, 출고일자, 출고여부를 조회하는 SQL문을 작성해주세요. 출고여부는 2022년 5월 1일까지 출고완료로 이 후 날짜는 출고 대기로 미정이면 출고미정으로 출력해주시고, 결과는 주문 ID를 기준으로 오름차순 정렬해주세요.



<br>

**Sample Input**

*FOOD_ORDER*
|ORDER_ID|	PRODUCT_ID|	AMOUNT|	PRODUCE_DATE|	IN_DATE|	OUT_DATE|	FACTORY_ID|	WAREHOUSE_ID|
|---|---|---|---|---|---|---|---|
|OD00000051|	P0002|	4000|	2022-04-01|	2022-04-21|	2022-04-21|	FT19970003|	WH0005|
|OD00000052|	P0003|	2500|	2022-04-10|	2022-04-27|	2022-04-27|	FT19970003|	WH0006|
|OD00000053|	P0005|	6200|	2022-04-15|	2022-04-30|	2022-05-01|	FT19940003	WH0003
|OD00000054|	P0006|	1000|	2022-04-21|	2022-04-30|	NULL|	FT19940003|	WH0009|
|OD00000055|	P0008|	1500|	2022-04-25|	2022-05-11|	2022-05-11|	FT19980003|	WH0009|
  
<br>

**Sample Output**

|ORDER_ID|	PRODUCT_ID|	OUT_DATE|	출고여부|
|---|---|---|---|
|OD00000051|	P0002|	2022-04-21|	출고완료|
|OD00000052|	P0003|	2022-04-27|	출고완료|
|OD00000053|	P0005|	2022-05-01|	출고완료|
|OD00000054|	P0006|		|출고미정|
|OD00000055|	P0008|	2022-05-11|	출고대기|

<br>

### Solving

```sql
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d') AS OUT_DATE
     , CASE 
            WHEN OUT_DATE <= '2022-05-01' THEN '출고완료'
            WHEN OUT_DATE IS NULL THEN '출고미정'
            ELSE '출고대기'
        END AS '출고여부'
FROM FOOD_ORDER
ORDER BY ORDER_ID
```
