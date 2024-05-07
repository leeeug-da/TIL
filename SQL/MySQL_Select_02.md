### Topic
- Select
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Weather Observation Station 6)
- *table* : STATION

**STATION**
|column|type|
|---|---|
|ID|NUMBER|
|CITY|VARCHAR2(21)|
|STATE|VARCHAR2(2)|
|LAT_N|NUMBER|
|LONG_W|NUMBER|



### Problem 
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.
LAT_N is the northern latitude and LONG_W is the western longitude.

### Solving

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
   OR CITY LIKE 'e%'
   OR CITY LIKE 'i%'
   OR CITY LIKE 'o%'
   OR CITY LIKE 'u%'
```

### Study Note
- 조건문 쓸 때 컬럼명을 매번 써주어야 함 ! 
  - 틀린 예시:
    ```sql
    SELECT DISTINCT CITY
    FROM STATION
    WHERE CITY LIKE 'a%' OR 'e%' OR 'i%' OR 'o%' OR 'u%'
    ```
  - 정답 예시:
    ```sql
    SELECT DISTINCT CITY
    FROM STATION
    WHERE CITY LIKE 'a%'
      OR CITY LIKE 'e%'
      OR CITY LIKE 'i%'
      OR CITY LIKE 'o%'
      OR CITY LIKE 'u%'
    ```
