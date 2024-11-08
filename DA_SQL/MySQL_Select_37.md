### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (특정 형질을 가지는 대장균 찾기)
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
대장균 개체의 크기를 내름차순으로 정렬했을 때 상위 0% ~ 25% 를 'CRITICAL', 26% ~ 50% 를 'HIGH', 51% ~ 75% 를 'MEDIUM', 76% ~ 100% 를 'LOW' 라고 분류합니다. 대장균 개체의 ID(`ID`) 와 분류된 이름(`COLONY_NAME`)을 출력하는 SQL 문을 작성해주세요. 이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요 . 단, 총 데이터의 수는 4의 배수이며 같은 사이즈의 대장균 개체가 서로 다른 이름으로 분류되는 경우는 없습니다.

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

기준에 의해 분류된 대장균들의 ID는 다음과 같습니다.

- CRITICAL (상위 0% ~ 25%) : ID 6, ID 7
- HIGH (상위 26% ~ 50%) : ID 3, ID 5
- MEDIUM (상위 51% ~ 75%) : ID 1, ID 4
- LOW (상위 76% ~ 100%) : ID 2, ID 8

따라서 결과를 ID 에 대해 오름차순 정렬하면 다음과 같아야 합니다.

<br>

**Sample Output**
|ID|	COLONY_NAME|
|---|---|
|1|	MEDIUM|
|2|	LOW|
|3|	HIGH|
|4|	MEDIUM|
|5|	HIGH|
|6|	CRITICAL|
|7|	CRITICAL|
|8|	LOW|

<br>

### Solving

```sql
SELECT ID, 
        CASE 
            WHEN S.RANKS/CNTS <= 0.25 THEN 'CRITICAL'
            WHEN S.RANKS/CNTS <= 0.5 THEN 'HIGH'
            WHEN S.RANKS/CNTS <= 0.75 THEN 'MEDIUM'
            ELSE 'LOW'
        END AS COLONY_NAME
FROM (SELECT * 
           , RANK() OVER(ORDER BY SIZE_OF_COLONY DESC) AS RANKS
           , COUNT(*) OVER() AS CNTS
          FROM ECOLI_DATA) AS S
ORDER BY ID
```
