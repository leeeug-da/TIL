### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 따릉이 자전거 이용 현황 
- *platform* : 데이터리안
- *table* : station

|column|type|description|  
|---|---|---|
|station_id|integer|정류소ID|
|name|string|정류소명|
|local|string|소속 지자체|
|address|string|주소|
|lat|string|위도(deg)|
|lng|string|경도(deg)|
|updated_at|date|정류소 최근 갱신 일자|
|type|string|정류소 타입 (LCD, QR)|




### Problem 
Q. station 테이블에는 따릉이 정류소에 대한 정보가 담겨있습니다. '서울북부지방법원' 정류소보다 북쪽에 있는 정류소 정보를 출력하는 쿼리를 작성해주세요. 쿼리 결과에는 station 테이블에 있는 모든 컬럼이 출력되어야 합니다.

### Solving
```sql
-- '북쪽에 있는' = 위도(lat)가 더 높은 
-- '서울북부지방법원' : name 컬럼 사용

SELECT *
FROM station
WHERE lat > (SELECT lat 
             FROM station 
             WHERE name = '서울북부지방법원')
```
