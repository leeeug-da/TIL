### Topic
- Aggregation
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql (데이터리안)
- *table* : tips

**tips**
|column|type|
|---|---|
|total_bill|number|
|tip|number|
|sex|string|
|smoker|string|
|day|string|
|time|string|
|size|integer|




### Problem 
`tips` 테이블에는 식사 금액, 팁, 결제자 성별, 요일, 시간대 등 어느 레스토랑의 테이블 당 결제에 관련된 데이터가 들어있습니다. 요일별 매출액 합계를 구하고, 매출이 1500 달러 이상인 요일의 결제 내역을 모두 출력하는 쿼리를 작성해주세요. 쿼리 결과에는 `tips` 테이블에 있는 모든 컬럼이 포함되어야 합니다.


### Solving

```sql
-- 매출이 1500달러 이상인 요일 찾기
SELECT day
     , SUM(total_bill) AS revenue
FROM tips
GROUP BY day

-- 1500 달러 이상인 요일 : Sun, Sat
SELECT *
FROM tips
WHERE day IN ('Sun', 'Sat')
```

