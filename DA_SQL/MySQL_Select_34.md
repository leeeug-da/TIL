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
2번 형질이 보유하지 않으면서 1번이나 3번 형질을 보유하고 있는 대장균 개체의 수(`COUNT`)를 출력하는 SQL 문을 작성해주세요. 1번과 3번 형질을 모두 보유하고 있는 경우도 1번이나 3번 형질을 보유하고 있는 경우에 포함합니다.

<br>

**Sample Input**

*ECOLI_DATA*
|ID|	PARENT_ID|	SIZE_OF_COLONY|	DIFFERENTIATION_DATE|	GENOTYPE|
|---|---|---|---|---|
|1|	NULL|	17|	2019/01/01|	5|
|2|	NULL|	150|	2019/01/01|	3|
|3|	1|	4000|	2020/01/01|	4|

<br>

각 대장균 별 형질을 2진수로 나타내면 다음과 같습니다.

- ID 1 : 1000₍₂₎
- ID 2 : 1111₍₂₎
- ID 3 : 1₍₂₎
- ID 4 : 1101₍₂₎

각 대장균 별 보유한 형질을 다음과 같습니다.

- ID 1 : 4
- ID 2 : 1, 2, 3, 4
- ID 3 : 1
- ID 4 : 1, 3, 4

따라서 2번 형질이 없는 대장균 개체는 ID 1, ID 3, ID 4 이며 이 중 1번이나 3번 형질을 보유한 대장균 개체는 ID 3, ID 4 입니다.

따라서 결과는 다음과 같아야 합니다.

<br>

**Sample Output**
|COUNT|
|---|
|2|

<br>

### Solving

```sql
SELECT COUNT(ID) AS COUNT
FROM ECOLI_DATA
WHERE (GENOTYPE&2 = 0) AND (GENOTYPE&1 = 1 OR GENOTYPE&4 = 4)
```
