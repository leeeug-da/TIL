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
`tips` 테이블에는 식사 금액, 팁, 결제자, 성별, 요일, 시간대 등 어느 레스토랑의 테이블 당 결제에 관련된 데이터가 들어있습니다.
이 레스토랑의 일일 평균 매출을 계산해주세요. 예를 들어, 일일 매출이 다음과 같다면 일일 평균 매출은 287.5 입니다. 컬럼의 이름은 `avg_sales`로 출력해주세요. 결과는 소수점 아래 셋째 자리에서 반올림하여 둘째 자리까지 표시되어야 합니다.

**Sample Input**
|day|sales|
|---|---|
|Thur|100|
|Fri|200|
|Sat|400|
|Sun|450|

**Sample Output**
|avg_sales|
|---|
|287.5|



### Solving

```sql
SELECT ROUND(SUM(total_bill) / COUNT(DISTINCT day), 2) AS avg_sales
FROM tips
```

