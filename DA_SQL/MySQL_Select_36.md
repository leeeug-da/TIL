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
부모의 형질을 모두 보유한 대장균의 ID(`ID`), 대장균의 형질(`GENOTYPE`), 부모 대장균의 형질(`PARENT_GENOTYPE`)을 출력하는 SQL 문을 작성해주세요. 이때 결과는 ID에 대해 오름차순 정렬해주세요.

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

각 대장균 별 형질을 2진수로 나타내면 다음과 같습니다.

- ID 1 : 1₍₂₎
- ID 2 : 1₍₂₎
- ID 3 : 11₍₂₎
- ID 4 : 10₍₂₎
- ID 5 : 1000₍₂₎
- ID 6 : 101₍₂₎
- ID 7 : 101₍₂₎
- ID 8 : 1101₍₂₎

각 대장균 별 보유한 형질을 다음과 같습니다.

- ID 1 : 1
- ID 2 : 1
- ID 3 : 1, 2
- ID 4 : 2
- ID 5 : 4
- ID 6 : 1, 3
- ID 7 : 1, 3
- ID 8 : 1, 3, 4

각 개체별로 살펴보면 다음과 같습니다.

- ID 1 : 최초의 대장균 개체이므로 부모가 없습니다.
- ID 2 : 부모는 ID 1 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
- ID 3 : 부모는 ID 1 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
- ID 4 : 부모는 ID 2 이며 부모의 형질인 1번 형질을 보유하고 있지 않습니다.
- ID 5 : 부모는 ID 4 이며 부모의 형질인 2번 형질을 보유하고 있지 않습니다.
- ID 6 : 부모는 ID 3 이며 부모의 형질 1, 2번 중 2 번 형질을 보유하고 있지 않습니다.
- ID 7 : 부모는 ID 2 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
- ID 8 : 부모는 ID 6 이며 부모의 형질 1, 3번을 모두 보유하고 있습니다.

따라서 부모의 형질을 모두 보유한 개체는 ID 2, ID 3, ID 7, ID 8 이며 결과를 ID 에 대해 오름차순 정렬하면 다음과 같아야 합니다.

<br>

**Sample Output**
|ID|	GENOTYPE|	PARENT_GENOTYPE|
|---|---|---|
|2|	1|	1|
|3|	3|	1|
|7|	5|	1|
|8|	13|	5|

<br>

### Solving

```sql
SELECT E1.ID
     , E1.GENOTYPE AS GENOTYPE
     , E2.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA E1 
  JOIN ECOLI_DATA E2 ON E1.PARENT_ID = E2.ID
WHERE (E1.GENOTYPE & E2.GENOTYPE) = E2.GENOTYPE
ORDER BY E1.ID ASC;
```
