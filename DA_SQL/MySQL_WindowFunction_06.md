### Topic
- Window Function (RANK 함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql (레스토랑의 요일별 VIP)
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


<br>

### Problem 
`tips` 테이블에는 식사 금액, 팁, 결제자 성별, 요일, 시간대 등 어느 레스토랑의 테이블 당 결제에 관련된 데이터가 들어있습니다. 요일별로 가장 높은 금액의 결제 내역을 출력하는 쿼리를 작성해주세요. 쿼리 결과에는 `tips` 테이블에 있는 모든 컬럼이 포함되어야 합니다.

<br>

**Sample Input**
|total_bill|tip|sex|smoker|day|time|size|
|---|---|---|---|---|---|---|
|16.99|1.01|Female|No|Sun|Dinner|2|
|10.34|1.66|Male|No|Sun|Dinner|3|
|21.01|3.5|Male|No|Sun|Dinner|3|
|23.68|3.31|Male|No|Sun|Dinner|2|

<br>

**Sample Output**
|total_bill|tip|sex|smoker|day|time|size|
|---|---|---|---|---|---|---|
|40.17|4.73|Male|Yes|Fri|Dinner|4|
|50.81|10|Male|Yes|Sat|Dinner|3|
|48.17|5|Male|No|Sun|Dinner|6|
|43.11|5|Female|Yes|Thur|Lunch|4|


<br>

### Solving
```sql
SELECT total_bill, tip, sex, smoker, day, time, size
FROM (
  SELECT *
      , ROW_NUMBER() OVER (PARTITION BY day ORDER BY total_bill DESC) AS rn
  FROM tips
) bill_stats
WHERE rn = 1
```
