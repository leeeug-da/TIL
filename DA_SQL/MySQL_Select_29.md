### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (잔챙이 잡은 수 구하기)
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
잡은 물고기 중 길이가 10cm 이하인 물고기의 수를 출력하는 SQL 문을 작성해주세요.

물고기의 수를 나타내는 컬럼 명은 FISH_COUNT로 해주세요.

<br>

**Sample Input**

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	13.37|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	43.33|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	NULL|	2020/04/28|

<br>

**Sample Output**
|FISH_COUNT|
|---|
|2|

<br>

### Solving

```sql
SELECT COUNT(DISTINCT ID) AS FISH_COUNT
FROM FISH_INFO
WHERE LENGTH IS NULL
```
