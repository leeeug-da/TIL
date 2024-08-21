### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
입양 시각 구하기(1))
- *table* : ANIMAL_OUTS

<br>

**ANIMAL_OUTS**
|column|type|nullable|
|---|---|---|
|ANIMAL_ID|	VARCHAR(N)|	FALSE|
|ANIMAL_TYPE|	VARCHAR(N)|	FALSE|
|DATETIME|	DATETIME|	FALSE|
|NAME|	VARCHAR(N)	|TRUE|
|SEX_UPON_OUTCOME|	VARCHAR(N)|	FALSE|


`ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.

<br>

### Problem
보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.



<br>

**Sample Output**

|HOUR|	COUNT|
|---|---|
|9|	1|
|10|	2|
|11|	13|
|12|	10|
|13|	14|
|14|	9|
|15|	7|
|16|	10|
|17|	12|
|18|	16|
|19|	2|

<br>

### Solving

```sql
SELECT HOUR(DATETIME) AS HOUR
     , COUNT(DISTINCT ANIMAL_ID) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) BETWEEN 9 AND 19
GROUP BY HOUR
ORDER BY HOUR
```