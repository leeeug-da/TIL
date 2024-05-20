### Topic
- Select
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Weather Observation Station 7)
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
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
LAT_N is the northern latitude and LONG_W is the western longitude.

### Solving

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[aeiou]$'
```

### Study Note
**정규표현식**

|`.`|문자 하나| "..." : 문자 길이가 3 이상인 문자|
|---|---|---|
|`[]`|안에 나열된 패턴에 해당하는 문자열|"[abc]1" : 문자열에서 'a1' 또는 'b1' 또는 'c1'인 문자열을 찾음|
|`^`|시작하는 문자열|"^안녕" : 문자열에서 '안녕'으로 시작하는 문자열을 찾음|
|`$`|끝나는 문자열|"잘가$" : 문자열에서 '잘가'로 끝나는 문자열을 찾음|
