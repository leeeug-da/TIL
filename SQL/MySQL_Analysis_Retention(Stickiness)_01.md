### Topic
- Retention (Stickiness)
  
### Language
- MySQL

### Data
- *database* : US E-Commerce Records 2020
- *platform* : 데이터리안
- *table* : records

|column|type|description|  
|---|---|---|
|date|order_date|주문 날짜|
|string|order_id|주문 ID|
|string|ship_mode|배송 타입|
|string|customer_id|고객 ID|
|string|segment|고객 타입|
|string|country|국가|
|string|city|도시|
|string|state|주|
|integer|postal_code|우편번호|
|string|region|지역|
|string|product_id|상품 ID|
|string|category|카테고리|
|string|sub_category|서브 카테고리|
|string|product_name|상품명|
|number|sales|매출|
|integer|quantity|수량|
|number|discount|할인|
|number|profit|이익|




### Problem 
US E-Commerce Records 2020 데이터셋은 미국의 온라인 쇼핑몰 2020년 판매 데이터 입니다. `records` 테이블에는 각 주문별로 주문 날짜, 주문된 상품의 정보, 가격 등이 기록되어있습니다.

온라인 쇼핑몰 데이터 팀에서 고객들의 재방문 정도를 확인하기 위해 Stickiness (고객 고착도)를 확인하려고 합니다. 

이 때 ‘활성'을 다양하게 정의할 수 있는데 분석하고자 하는 온라인 쇼핑몰에서는 주문 완료 액션을 중요하게 생각하기 때문에 해당 기간 동안 한 번이라도 주문한 고객을 ‘활성 고객'으로 정의합니다.

`records` 테이블을 이용하여 2020년 11월 한 달 동안의 일별 DAU, WAU, Stickiness를 계산하는 쿼리를 작성해주세요. 쿼리 결과는 아래 네 개의 컬럼을 포함해야 합니다. `stickiness` 는 반올림하여 소수점 둘째자리까지만 출력해주세요. 고객들이 한번도 주문을 하지 않은 날은 집계에서 제외하며, `dt` 컬럼을 기준으로 오름차순 정렬해주세요.

- `dt` - 기준 날짜
- `dau` - 기준 날짜에 주문한 고객 수
- `wau` - 기준 날짜 6일 전부터 해당 날짜까지 상품을 주문한 고객 수
- `stickiness` - 기준 날짜의 고객 고착도

**출력 예시 및 설명**

|dt|dau|wau|stickiness|
|---|---|---|---|
|2020-11-06|13|59|0.22|
|2020-11-07|7|64|0.11|

2020년 11월 7일의 DAU는 해당 날짜에 주문을 했던 고객의 수이고, 2020년 11월 7일의 WAU는 2020년 11월 1일부터 11월 7일 사이에 한 번이라도 주문한 고객의 수 입니다. 2020년 11월 7일의 Stickiness는 WAU 대비 DAU의 비율입니다.

### Solving
- 활성의 기준 : 주문
- 날짜 : 2020년 11월 
- dt : 기준 날짜 (오름차순 정렬)
- dau : 기준 날짜에 주문한 고객 수
- wau : 기준 날짜 6일 전부터 해당 날짜까지 주문한 고객 수
- stickiness : DAU/WAU,  반올림 소수점 2자리
  

`ver1`
```sql
WITH au_stats AS (
  SELECT order_date AS dt
      , COUNT(DISTINCT customer_id) AS dau
      , (SELECT COUNT(DISTINCT customer_id)
          FROM records r2
          WHERE r2.order_date BETWEEN DATE_SUB(r1.order_date, INTERVAL 6 DAY) AND r1.order_date
        ) AS wau
  FROM records r1
  WHERE order_date BETWEEN '2020-11-01' AND '2020-11-30'
  GROUP BY order_date
  ORDER BY order_date
)

SELECT dt
     , dau
     , wau
     , ROUND((dau/wau), 2) AS stickiness
FROM au_stats
```

`ver2`
```sql
SELECT d.order_date AS dt
     , COUNT(DISTINCT d.customer_id) AS dau
     , COUNT(DISTINCT w.customer_id) AS wau
     , ROUND(COUNT(DISTINCT d.customer_id) / COUNT(DISTINCT w.customer_id), 2) AS stickiness
FROM records AS d
  LEFT JOIN records AS w ON w.order_date BETWEEN DATE_ADD(d.order_date, INTERVAL -6 DAY) AND d.order_date
WHERE d.order_date BETWEEN '2020-11-01' AND '2020-11-30'
GROUP BY d.order_date
```
