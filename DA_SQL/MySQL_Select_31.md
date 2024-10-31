### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (특정 물고기를 잡은 총 수 구하기)
- *table* : FISH_INFO, FISH_NAME_INFO

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

**FISH_NAME_INFO**
|column|type|nullable|
|---|---|---|
|FISH_TYPE|	INTEGER|	FALSE|
|FISH_NAME|	VARCHAR|	FALSE|

`FISH_NAME_INFO` 테이블의 구조는 다음과 같으며, `FISH_TYPE`, `FISH_NAME` 은 각각 물고기의 종류(숫자), 물고기의 이름(문자) 입니다.

<br>

### Problem
`FISH_INFO` 테이블에서 잡은 `BASS`와 `SNAPPER`의 수를 출력하는 SQL 문을 작성해주세요.

컬럼명은 'FISH_COUNT`로 해주세요.

<br>

**Sample Input**

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	30|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	20|	2022/03/09
|4|	1|	NULL|	2022/04/08|
|5|	2|	13|	2021/04/28|
|6|	3|	60|	2021/07/27|
|7|	0|	55|	2021/01/18|
|8|	2|	73|	2020/01/28|
|9|	3	73|	2021/04/08|
|10|	2|	22|	2020/06/28|
|11|	2|	17|	2022/12/23|

<br>

*FISH_NAME_INFO*
|FISH_TYPE|	FISH_NAME|
|---|---|
|0|	BASS|
|1|	SNAPPER|
|2|	ANCHOVY|


<br> 

**Sample Output**
|FISH_COUNT|
|---|
|7|

<br>

### Solving

```sql
SELECT COUNT(DISTINCT FI.ID) AS FISH_COUNT
FROM FISH_INFO FI
INNER JOIN FISH_NAME_INFO FN USING (FISH_TYPE)
WHERE FN.FISH_NAME IN ('BASS', 'SNAPPER')
```
