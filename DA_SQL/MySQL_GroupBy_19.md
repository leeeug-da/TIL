### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
물고기 종류 별 잡은 수 구하기)
- *table* : FISH_NAME_INFO, FISH_INFO

<br>

**FISH_NAME_INFO**
|column|type|nullable|
|---|---|---|
|ID|	INTEGER|	FALSE|
|FISH_TYPE|	INTEGER|	FALSE|
|LENGTH|	FLOAT|	TRUE|
|TIME|	DATE|	FALSE|

<br>

**FISH_INFO**
|column|type|nullable|
|---|---|---|
|FISH_TYPE|	INTEGER|	FALSE|
|FISH_NAME|	VARCHAR|	FALSE|


### Problem
`FISH_NAME_INFO에서` 물고기의 종류 별 물고기의 이름과 잡은 수를 출력하는 SQL문을 작성해주세요.

물고기의 이름 컬럼명은 `FISH_NAME`, 잡은 수 컬럼명은 `FISH_COUNT`로 해주세요.
결과는 잡은 수 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*FISH_NAME_INFO*
|FISH_TYPE|	FISH_NAME|
|---|---|
|0|	BASS|
|1|	SNAPPER|
|2|	ANCHOVY|

<br>

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	13.37|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	43.33|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	32|	2020/04/28|

<br>

**Sample Output**

|FISH_COUNT|	FISH_NAME|
|---|---|
|3|	BASS|
|2|	SNAPPER|
|1|	ANCHOVY|

<br>

### Solving

```sql
WITH COUNT_FISH AS (
    SELECT FISH_TYPE
         , COUNT(FISH_TYPE) AS FISH_COUNT
    FROM FISH_INFO
    GROUP BY FISH_TYPE
)

SELECT C.FISH_COUNT
     , F.FISH_NAME
FROM COUNT_FISH C
 LEFT JOIN FISH_NAME_INFO F ON F.FISH_TYPE = C.FISH_TYPE 
ORDER BY C.FISH_COUNT DESC
```
