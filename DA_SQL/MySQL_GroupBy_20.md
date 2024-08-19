### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
월별 잡은 물고기 수 구하기)
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
월별 잡은 물고기의 수와 월을 출력하는 SQL문을 작성해주세요.

잡은 물고기 수 컬럼명은 `FISH_COUNT`, 월 컬럼명은 `MONTH`로 해주세요.
결과는 월을 기준으로 오름차순 정렬해주세요.
단, 월은 숫자형태 (1~12) 로 출력하며 9 이하의 숫자는 두 자리로 출력하지 않습니다. 잡은 물고기가 없는 월은 출력하지 않습니다.

<br>

**Sample Input**

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	30|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	20|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	13|	2021/04/28|
|6|	3|	60|	2021/07/27|

<br>

**Sample Output**

|FISH_COUNT|	MONTH|
|---|---|
|2|	1|
|3|	3|
|3|	4|
|1|	6|
|1|	7|
|2|	12|

<br>

### Solving

```sql
SELECT COUNT(FISH_TYPE) AS FISH_COUNT
     , MONTH(TIME) AS MONTH
FROM FISH_INFO
GROUP BY MONTH(TIME)
HAVING COUNT(FISH_TYPE) IS NOT NULL
ORDER BY MONTH(TIME)
```
