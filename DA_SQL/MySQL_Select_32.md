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
대장균 개체의 ID(`ID`)와 자식의 수(`CHILD_COUNT`)를 출력하는 SQL 문을 작성해주세요. 자식이 없다면 자식의 수는 0으로 출력해주세요. 이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

<br>

**Sample Input**

*ECOLI_DATA*
|ID|	PARENT_ID|	SIZE_OF_COLONY|	DIFFERENTIATION_DATE|	GENOTYPE|
|---|---|---|---|---|
|1|	NULL|	10|	2019/01/01|	5|
|2|	NULL|	2|	2019/01/01|	3|
|3|	1|	100|	2020/01/01|	4|
|4|	2|	17|	2020/01/01|	4|
|5|	2|	10|	2020/01/01|	6|
|6|	4|	101|	2021/01/01|	22|

<br>

**Sample Output**
|ID|	CHILD_COUNT|
|---|---|
|1|	1|
|2|	2|
|3|	0|
|4|	1|
|5|	0|
|6|	0|

<br>

### Solving

```sql
SELECT A.ID, COUNT(B.ID) AS CHILD_COUNT
FROM ECOLI_DATA A
 LEFT JOIN ECOLI_DATA B ON A.ID = B.PARENT_ID
GROUP BY A.ID
ORDER BY A.ID
```
