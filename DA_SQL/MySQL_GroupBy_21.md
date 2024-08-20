### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
특정 조건을 만족하는 물고기별 수와 최대 길이 구하기)
- *table* : FISH_INFO

<br>

**FISH_INFO**
|column|type|nullable|
|---|---|---|
|ID|	INTEGER|	FALSE|
|FISH_TYPE|	INTEGER|	FALSE|
|LENGTH|	FLOAT|	TRUE|
|TIME|	DATE|	FALSE|


### Problem
`FISH_INFO`에서 평균 길이가 33cm 이상인 물고기들을 종류별로 분류하여 잡은 수, 최대 길이, 물고기의 종류를 출력하는 SQL문을 작성해주세요. 결과는 물고기 종류에 대해 오름차순으로 정렬해주시고, 10cm이하의 물고기들은 10cm로 취급하여 평균 길이를 구해주세요.

컬럼명은 물고기의 종류 'FISH_TYPE', 잡은 수 'FISH_COUNT', 최대 길이 'MAX_LENGTH'로 해주세요.

<br>

**Sample Input**

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	30|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	30|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	32|	2021/04/28|

<br>

**Sample Output**

|FISH_COUNT|	MAX_LENGTH|	FISH_TYPE|
|---|---|---|
|3|	50|	0|

<br>

### Solving

```sql
WITH LENGTH_10 AS (
    SELECT ID
         , FISH_TYPE
         , CASE
                WHEN LENGTH <= 10 THEN 10
                WHEN LENGTH IS NULL THEN 10
                ELSE LENGTH 
           END AS LENGTH2
         , TIME 
     FROM FISH_INFO
)

SELECT COUNT(ID) AS FISH_COUNT
     , MAX(LENGTH2) AS MAX_LENGTH
     , FISH_TYPE
FROM LENGTH_10
GROUP BY FISH_TYPE
HAVING AVG(LENGTH2) >= 33
ORDER BY FISH_TYPE
```
