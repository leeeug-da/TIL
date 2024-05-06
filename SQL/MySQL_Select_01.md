### Topic
- Select
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Weather Observation Station 5)
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
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically. LAT_N is the northern latitude and LONG_W is the western longitude.

**Sample Input**

For example, CITY has four entries: DEF, ABC, PQRS and WXY.

**Sample Output**

ABC 3 <br/>
PQRS 4 <br/>

**Explanation**

When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with lengths  and . The longest name is PQRS, but there are  options for shortest named city. Choose ABC, because it comes first alphabetically.

### Solving

```sql
SELECT CITY
     , LENGTH(CITY)
FROM STATION
GROUP BY CITY
ORDER BY LENGTH(CITY) ASC, CITY ASC
LIMIT 1;

SELECT CITY
     , LENGTH(CITY)
FROM STATION
GROUP BY CITY
ORDER BY LENGTH(CITY) DESC, CITY ASC
LIMIT 1;
```

### Study Note
- ORDER BY 컬럼 순서를 어떻게 하냐에 따라 결과가 다르게 나온다.
  - 틀린 예시:
    ```sql
    ORDER BY CITY ASC, LENGTH(CITY) ASC
    ORDER BY CITY ASC, LENGTH(CITY) DESC
    ```
  - 정답 예시:
    ```sql
    ORDER BY LENGTH(CITY) ASC, CITY ASC
    ORDER BY LENGTH(CITY) DESC, CITY ASC
    ```
