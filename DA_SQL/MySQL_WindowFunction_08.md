### Topic
- Window Function (집계함수)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (Sum, Max, Min) (연도별 대장균 크기의 편차 구하기)
- *table* : ECOLI_DATA

**ECOLI_DATA**
|column|type|
|---|---|
|ID|INTEGER|
|PARENT_ID|INTEGER|
|SIZE_OF_COLONY|INTEGER|
|DIFFERENTIATION_DATE|DATE|
|GENOTYPE|INTEGER|

대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
다음은 실험실에서 배양한 대장균들의 정보를 담은 `ECOLI_DATA` 테이블입니다. `ECOLI_DATA` 테이블의 구조는 다음과 같으며, `ID`, `PARENT_ID`, `SIZE_OF_COLONY`, `DIFFERENTIATION_DATE`, `GENOTYPE` 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다. 최초의 대장균 개체의 `PARENT_ID` 는 NULL 값입니다.


<br>

### Problem 
분화된 연도(`YEAR`), 분화된 연도별 대장균 크기의 편차(`YEAR_DEV`), 대장균 개체의 ID(`ID`) 를 출력하는 SQL 문을 작성해주세요. 분화된 연도별 대장균 크기의 편차는 분화된 연도별 가장 큰 대장균의 크기 - 각 대장균의 크기로 구하며 결과는 연도에 대해 오름차순으로 정렬하고 같은 연도에 대해서는 대장균 크기의 편차에 대해 오름차순으로 정렬해주세요.

<br>

**Sample Input**
|ID|PARENT_ID|SIZE_OF_COLONY|DIFFERENTIATION_DATE|GENOTYPE|
|---|---|---|---|---|
|1|	NULL|	10|	2019/01/01|	5|
|2|	NULL|	2|	2019/01/01|	3|
|3|	1|	100|	2020/01/01|	4|
|4|	2|	10|	2020/01/01|	4|
|5|	2|	17|	2020/01/01|	6|
|6|	4|	101|	2021/01/01|	22|


분화된 연도별 가장 큰 대장균의 크기는 다음과 같습니다.
- 2019 : 10
- 2020 : 100
- 2021 : 101

따라서 각 대장균의 분화된 연도별 대장균 크기의 편차는 다음과 같습니다.
- ID 1 : 10 - 10 = 0
- ID 2 : 10 -2 = 8
- ID 3 : 100 - 100 = 0
- ID 4 : 100 - 10 = 90
- ID 5 : 100 - 17 = 83
- ID 6 : 101 -101 - 0

이를 분화된 연도에 대해 오름차순으로 정렬하고 같은 연도에 대해서는 대장균 크기의 편차에 대해 오름차순으로 정렬하면 결과는 다음과 같아야 합니다.

<br>

**Sample Output**
|YEAR|	YEAR_DEV|	ID|
|---|---|---|
|2019|	0|	1|
|2019|	8|	2|
|2020|	0|	3|
|2020|	83|	5|
|2020|	90|	4|
|2021|	0|	6|


<br>

### Solving

**<윈도우 함수 풀이>**
```sql
SELECT YEAR(DIFFERENTIATION_DATE) AS YEAR
, (MAX(SIZE_OF_COLONY) OVER (PARTITION BY YEAR(DIFFERENTIATION_DATE))) - SIZE_OF_COLONY AS YEAR_DEV
, ID 
FROM ECOLI_DATA
ORDER BY YEAR, YEAR_DEV
```


**<WITH문 풀이>**
```sql
-- 1. 분화된 연도별 가장 큰 대장균의 크기
WITH MAX_COLONY AS (
    SELECT YEAR(DIFFERENTIATION_DATE) AS YEAR
         , MAX(SIZE_OF_COLONY) AS MAX_SIZE
    FROM ECOLI_DATA
    GROUP BY YEAR
)
-- 2. 메인쿼리
SELECT M.YEAR
     , M.MAX_SIZE - E.SIZE_OF_COLONY AS YEAR_DEV
     , E.ID
FROM ECOLI_DATA E
 INNER JOIN MAX_COLONY M ON YEAR(E.DIFFERENTIATION_DATE) = M.YEAR
WHERE YEAR(E.DIFFERENTIATION_DATE) = M.YEAR
ORDER BY M.YEAR, YEAR_DEV
```
