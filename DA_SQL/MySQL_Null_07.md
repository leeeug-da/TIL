### Topic
- NULL
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (IS NULL) (
잡은 물고기의 평균 길이 구하기)
- *table* : FISH_INFO

<br>

**FISH_INFO**
|column|type|nullable|
|---|---|---|
|ID|	INTEGER|	FALSE|
|FISH_TYPE|	INTEGER|	FALSE|
|LENGTH|	FLOAT|	TRUE|
|TIME|	DATE|	FALSE|

`FISH_INFO` 테이블의 구조는 다음과 같으며 `ID`, `FISH_TYPE`, `LENGTH`, `TIME`은 각각 잡은 물고기의 ID, 물고기의 종류(숫자), 잡은 물고기의 길이(cm), 물고기를 잡은 날짜를 나타냅니다.

단, 잡은 물고기의 길이가 10cm 이하일 경우에는 `LENGTH` 가 NULL 이며, `LENGTH` 에 NULL 만 있는 경우는 없습니다.


<br>

### Problem
잡은 물고기의 평균 길이를 출력하는 SQL문을 작성해주세요.

평균 길이를 나타내는 컬럼 명은 AVERAGE_LENGTH로 해주세요.
평균 길이는 소수점 3째자리에서 반올림하며, 10cm 이하의 물고기들은 10cm 로 취급하여 평균 길이를 구해주세요.

<br>

**Sample Input**

*IFISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	30|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	20|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	NULL|	2021/04/28|

<br>

**Sample Output**

|AVERAGE_LENGTH|
|---|
|26.67|

<br>

### Solving

```sql
WITH LENGTH2 AS (
SELECT *
     , CASE
            WHEN LENGTH IS NULL THEN 10 
            ELSE LENGTH
       END AS LENGTH2
FROM FISH_INFO
)

SELECT ROUND(AVG(LENGTH2), 2) AS AVERAGE_LENGTH
FROM LENGTH2
```
