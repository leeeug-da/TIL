### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (특정 세대의 대장균 찾기)
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
3세대의 대장균의 ID(`ID`) 를 출력하는 SQL 문을 작성해주세요. 이때 결과는 대장균의 ID 에 대해 오름차순 정렬해주세요.

<br>

**Sample Input**

*ECOLI_DATA*
|ID|	PARENT_ID|	SIZE_OF_COLONY|	DIFFERENTIATION_DATE|	GENOTYPE|
|---|---|---|---|---|
|1|	NULL|	10|	2019/01/01|	1|
|2|	1|	2|	2019/01/01|	1|
|3|	1|	100|	2020/01/01|	3|
|4|	2|	16|	2020/01/01|	2|
|5|	4|	17|	2020/01/01|	8|
|6|	3|	101|	2021/01/01|	5|
|7|	2|	101|	2022/01/01|	5|
|8|	6|	1|	2022/01/01|	13|

<br>

PARENT ID 가 NULL 인 ID 1, ID 2가 1 세대이며 ID 1에서 분화된 ID 3, ID 2에서 분화된 ID 4, ID 5 가 2 세대입니다. ID 4 에서 분화된 ID 6, ID 3에서 분화된 ID 7 이 3 세대이며 ID 6에서 분화된 ID 8은 4 세대입니다.

따라서 결과를 ID 에 대해 오름차순 정렬하면 다음과 같아야 합니다.

<br>

**Sample Output**
|ID|
|---|
|6|
|7|

<br>

### Solving

```sql
SELECT A.ID
FROM ECOLI_DATA A
 JOIN ECOLI_DATA B ON A.PARENT_ID = B.ID
 JOIN ECOLI_DATA C ON B.PARENT_ID = C.ID
WHERE C.PARENT_ID IS NULL
ORDER BY ID
```
