### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (한 해에 잡은 물고기 수 구하기)
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

<br>

### Problem
`FISH_INFO` 테이블에서 2021년도에 잡은 물고기 수를 출력하는 SQL 문을 작성해주세요.
이 때 컬럼명은 'FISH_COUNT' 로 지정해주세요.



<br>

**Sample Input**

*FISH_INFO*
|ID|	FISH_TYPE|	LENGTH|	TIME|
|0|	0|	13.37|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	43.33|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	NULL|	2021/04/28|
  
<br>

**Sample Output**

|FISH_COUNT|
|---|
|2|

<br>

### Solving

```sql
SELECT COUNT(ID) AS FISH_COUNT
FROM FISH_INFO
WHERE YEAR(TIME) = 2021
GROUP BY YEAR(TIME)
```
