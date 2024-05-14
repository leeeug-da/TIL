### Topic
- Case
  
### Language
- MySQL

### Data
- *database* : Brazilian E-Commerce Public Dataset by Olist
- *platform* : solvesql (데이터리안)
- *table* : olist_orders_dataset

|column|type|
|---|---|
|order_id|string|
|customer_id|string|
|order_status|string|
|order_purchase_timestamp|datetime|
|order_approved_at|datetime|
|order_delivered_carrier_date|datetime|
|order_delivered_customer_date|datetime|
|order_estimated_delivery_date|datetime|




### Problem 
Brazilian E-Commerce Public Dataset by Olist 데이터셋은 브라질의 이커머스 웹사이트인 Olist Store의 판매 데이터 입니다. <br>
그 중 `olist_orders_dataset` 테이블에는 주문 ID, 고객 ID, 주문 상태, 구매 시각 등 주문 내역 데이터가 들어있습니다. Olist의 주문부터 배송까지 프로세스는 다음 단계를 통해 이루어지고, 각 단계마다 시각을 기록하고 있습니다. <br>
1. 고객의 구매
   - `order_purchase_timestamp` 컬럼에 구매 시점이 저장됨
2. 판매자가 주문을 승인
   - `order_approved_at` 컬럼에 승인 시점이 저장됨
3. 택배사에 도착하여 배송 시작
    - `order_delivered_carrier_date` 컬럼에 배송 시작 시점이 저장됨
4. 배송 완료
    - `order_delivered_customer_date` 컬럼에 배송 완료 시점이 저장됨 <br>
  
추가로 `order_estimated_delivery_date` 컬럼에는 주문 시점에 계산한 배송 예정 시각이 저장되어 있습니다. <br>

2017년 1월 한 달 동안 발생한 주문의 배송 예측이 정확했는지 분석을 하려고 합니다. 고객의 구매 일자별로 배송 예정 시각 안에 고객에게 도착한 주문과, 배송 예정 시각이 지나서 고객에게 도착한 주문을 각각 집계하는 쿼리를 작성해주세요. <br>

배송 완료 또는 배송 예정 시각 데이터가 없는 경우는 계산에서 제외합니다. 계산 결과는 구매 날짜를 기준으로 오름차순 정렬되어야 하고, 아래 컬럼을 포함해야 합니다.

- `purchase_date` - 구매 날짜 (예: 2017-01-01)
- `success` - 배송 예정 시각 안에 고객에게 도착한 주문 수
- `fail` - 배송 예정 시각이 지나 고객에게 도착한 주문 수

<br>

**Sample Output**

|purchase_date|success|fail|
|---|---|---|
|2017-01-06|4|0|
|2017-01-07|3|1|



### Solving

```sql
-- 구매 시점 : order_purchase_timestamp
-- 배송 완료 시점 : order_delivered_customer_date
-- 배송 예정 시각 : order_estimated_delivery_date
-- 2017년 1월 한 달 동안

SELECT DATE(order_purchase_timestamp) AS purchase_date
     , COUNT(DISTINCT CASE 
                WHEN order_delivered_customer_date <= order_estimated_delivery_date
                THEN order_id END) AS success
     , COUNT(DISTINCT CASE 
                WHEN order_delivered_customer_date > order_estimated_delivery_date
                THEN order_id END) AS fail
FROM olist_orders_dataset
WHERE order_purchase_timestamp BETWEEN '2017-01-01 00:00:00' AND '2017-01-31 23:59:59'
  AND order_delivered_customer_date IS NOT NULL
  AND order_estimated_delivery_date IS NOT NULL
GROUP BY purchase_date
ORDER BY purchase_date ASC
```

