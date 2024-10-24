### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (조건에 맞는 회원수 구하기)
- *table* : USER_INFO

<br>

**USER_INFO**
|column|type|nullable|
|---|---|---|
|USER_ID|	INTEGER|	FALSE|
|GENDER|	TINYINT(1)|	TRUE|
|AGE|	INTEGER|	TRUE|
|JOINED|	DATE|	FALSE|

`USER_INFO` 테이블은 아래와 같은 구조로 되어있으며 `USER_ID`, `GENDER`, `AGE`, `JOINED`는 각각 회원 ID, 성별, 나이, 가입일을 나타냅니다.

<br>

### Problem
`USER_INFO` 테이블에서 2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력하는 SQL문을 작성해주세요.

<br>

**Sample Input**

*USER_INFO*
|USER_ID|	GENDER|	AGE|	JOINED|
|---|---|---|---|
|1|	1|	26|	2021-10-05|
|2|	0|	NULL|	2021-11-25|
|3|	1|	22|	2021-11-30|
|4|	0|	31|	2021-12-03|
|5|	0|	28|	2021-12-16|
|6|	1|	24|	2022-01-03|
|7|	1|	NULL|	2022-01-09|
<br>

**Sample Output**
|USERS|
|---|
|3|

<br>

### Solving

```sql
SELECT COUNT(DISTINCT USER_ID) AS USERS
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND YEAR(JOINED) = 2021
```
