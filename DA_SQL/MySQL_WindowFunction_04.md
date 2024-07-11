### Topic
- Window Function (RANK 함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql (레스토랑 요일 별 구매금액 Top 3 영수증)
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
|size|integer


<br>

### Problem 
`tips` 테이블에는 식사 금액, 팁, 결제자 성별, 결제 요일 등 레스토랑 손님들의 결제 영수증 정보가 들어있습니다.
레스토랑의 매니저는 요일 별로 큰 금액을 결제한 영수증을 찾고 싶습니다. 요일 별 결제 금액으로 Top 3 를 지불한 영수증을 출력해주세요. 결제 금액은 `total_bill` 컬럼에 있습니다.
예를 들어 금요일 손님들의 결제 금액이 각각 $10, $9, $9, $8, $5, $2 였다면 상위 결제 금액 3개는 $10, $9, $8입니다. 따라서 결제 금액이 $10, $9, $9, $8인 총 4개의 영수증을 각각 출력해야 합니다. 결과 데이터에는 아래 컬럼들이 포함되어야 합니다.

- `day` - 요일
- `time` - 시간대
- `sex` - 결제자 성별
- `total_bill` - 식사 금액 ($)

<br>

**Sample Input**
|total_bill|tip|sex|smoker|day|time|size|
|---|---|---|---|---|---|---|
|16.99|1.01|Female|No|Sun|Dinner|2|
|10.34|1.66|Male|No|Sun|Dinner|3|
|21.01|3.5|Male|No|Sun|Dinner|3|
|23.68|3.31|Male|No|Sun|Dinner|2|
|24.59|3.61|Female|No|Sun|Dinner|4|

<br>

**Sample Output**
|day|time|sex|total_bill|
|---|---|---|---|
|Fri|Dinner|Male|40.17|
|Fri|Dinner|Male|28.97|
|Fri|Dinner|Male|27.28|
|Sat|Dinner|Male|50.81|
|Sat|Dinner|Male|48.33|
|Sat|Dinner|Male|48.27|


<br>

### Solving
```sql
SELECT day, time, sex, total_bill
FROM (
  SELECT *
      , DENSE_RANK() OVER (PARTITION BY day ORDER BY total_bill DESC) AS rn
  FROM tips
  ) tips_rn
WHERE rn <= 3
```
