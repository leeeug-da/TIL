### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (대장균들의 자식의 수 구하기)
- *table* : ECOLI_DATA

<br>

**ECOLI_DATA**
|column|type|nullable|
|---|---|---|
|ID|	INTEGER|	FALSE|
|PARENT_ID|	INTEGER|	TRUE|
|SIZE_OF_COLONY|	INTEGER|	FALSE|
|DIFFERENTIATION_DATE|	DATE|	FALSE|
|GENOTYPE|	INTEGER|	FALSE|


다음은 실험실에서 배양한 대장균들의 정보를 담은 `ECOLI_DATA` 테이블입니다. `ECOLI_DATA` 테이블의 구조는 다음과 같으며, `ID`, `PARENT_ID`, `SIZE_OF_COLONY`, `DIFFERENTIATION_DATE`, `GENOTYPE` 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.

<br>

### Problem
대장균 개체의 크기가 100 이하라면 'LOW', 100 초과 1000 이하라면 'MEDIUM', 1000 초과라면 'HIGH' 라고 분류합니다. 대장균 개체의 ID(`ID`) 와 분류(`SIZE`)를 출력하는 SQL 문을 작성해주세요.이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

<br>

**Sample Input**

*ECOLI_DATA*
|ID|	PARENT_ID|	SIZE_OF_COLONY|	DIFFERENTIATION_DATE|	GENOTYPE|
|---|---|---|---|---|
|1|	NULL|	17|	2019/01/01|	5|
|2|	NULL|	150|	2019/01/01|	3|
|3|	1|	4000|	2020/01/01|	4|

<br>

**Sample Output**
|ID|	SIZE|
|---|---|
|1|	LOW|
|2|	MEDIUM|
|3|	HIGH|

<br>

### Solving

```sql
SELECT ID
     , CASE 
            WHEN SIZE_OF_COLONY <= 100 THEN 'LOW'
            WHEN SIZE_OF_COLONY <= 1000 THEN 'MEDIUM'
            ELSE 'HIGH'
       END AS 'SIZE'
FROM ECOLI_DATA
ORDER BY ID
```
