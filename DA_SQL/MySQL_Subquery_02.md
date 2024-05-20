### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : Waiter's Tips
- *platform* : 데이터리안
- *table* : tips

|column|type|description|  
|---|---|---|
|total_bill|number|식사 금액($)|
|tip|number|팁($)|
|sex|string|결제자 성별|
|smoker|string|일행 중 흡연자 존재 여부|
|day|string|요일|
|time|string|시간대|
|size|integer|일행 수(명)|




### Problem 
Q. tips 테이블에는 식사 금액, 팁, 결제자 성별, 요일, 시간대, 일행 수 등 어느 레스토랑의 테이블 당 결제에 관련된 데이터가 들어있습니다. 레스토랑에 함께 방문한 일행 수가 많아질수록 높은 금액을 결제하는지 알고 싶습니다. 결제 내역을 조회해 일행 수 마다 결제 금액이 가장 높았던 결제 내역만 출력하는 쿼리를 작성해주세요. 쿼리 결과에는 tips 테이블에 있는 모든 컬럼이 포함되어야 하며, 일행의 수가 작은 순서대로 출력되어야 합니다.

### Solving
```sql
-- 1) 결제 내역을 조회해 일행 수 마다 결제 금액이 가장 높았던 결제 내역 찾기
SELECT size, MAX(total_bill)
FROM tips
GROUP BY size
ORDER BY size ASC

--2) Subquery
SELECT *
FROM tips
WHERE (size, total_bill) IN (
  SELECT size
       , MAX(total_bill)
  FROM tips
  GROUP BY size 
)
ORDER BY size ASC 
```
