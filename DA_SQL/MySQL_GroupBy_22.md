### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
연간 평가점수에 해당하는 평가 등급 및 성과금 조회하기)
- *table* : HR_EMPLOYEES, HR_GRADE

<br>

**HR_EMPLOYEES**
|column|type|nullable|
|---|---|---|
|EMP_NO|	VARCHAR|	FALSE|
|EMP_NAME|	VARCHAR|	FALSE|
|DEPT_ID|	VARCHAR|	FALSE|
|POSITION|	VARCHAR|	FALSE|
|EMAIL|	VARCHAR|	FALSE|
|COMP_TEL|	VARCHAR|	FALSE|
|HIRE_DATE|	DATE|	FALSE|
|SAL|	NUMBER|	FALSE|

`HR_EMPLOYEES` 테이블은 회사의 사원 정보를 담은 테이블입니다. `HR_EMPLOYEES` 테이블의 구조는 다음과 같으며 `EMP_NO`, `EMP_NAME`, `DEPT_ID`, `POSITION`, `EMAIL`, `COMP_TEL`, `HIRE_DATE`, `SAL`은 각각 사번, 성명, 부서 ID, 직책, 이메일, 전화번호, 입사일, 연봉을 의미합니다.

<br>

**HR_GRADE**
|column|type|nullable|
|---|---|---|
|EMP_NO|	VARCHAR|	FALSE|
|YEAR|	NUMBER|	FALSE|
|HALF_YEAR|	NUMBER|	FALSE|
|SCORE|	NUMBER|	FALSE|

`HR_GRADE` 테이블은 2022년 사원의 평가 정보를 담은 테이블입니다. `HR_GRADE`의 구조는 다음과 같으며 `EMP_NO`, `YEAR`, `HALF_YEAR`, `SCORE`는 각각 사번, 연도, 반기, 평가 점수를 의미합니다.

### Problem
`HR_DEPARTMENT`, `HR_EMPLOYEES`, `HR_GRADE `테이블을 이용해 사원별 성과금 정보를 조회하려합니다. 평가 점수별 등급과 등급에 따른 성과금 정보가 아래와 같을 때, 사번, 성명, 평가 등급, 성과금을 조회하는 SQL문을 작성해주세요.

평가등급의 컬럼명은 `GRADE`로, 성과금의 컬럼명은 `BONUS`로 해주세요.
결과는 사번 기준으로 오름차순 정렬해주세요.

|기준 점수|	평가 등급|	성과금(연봉 기준)|
|---|---|---|
|96 이상|	S|	20%|
|90 이상|	A|	15%|
|80 이상|	B|	10%|
|이외|	C|	0%|

<br>

**Sample Input**

*HR_EMPLOYEES*
|EMP_NO|	EMP_NAME|	DEPT_ID|	POSITION|	EMAIL|	COMP_TEL|	HIRE_DATE|	SAL|
|---|---|---|---|---|---|--|---|
|2017002|	정호식|	D0001|	팀장|	hosick_jung@grep.com|	031-8000-1101|	2017-03-01|	65000000|
|2018001|	김민석|	D0001|	팀원|	minseock_kim@grep.com|	031-8000-1102|	2018-03-01|	60000000|
|2019001|	김솜이|	D0002|	팀장|	somi_kim@grep.com|	031-8000-1106|	2019-03-01|	60000000|
|2020002|	김연주|	D0002|	팀원|	yeonjoo_kim@grep.com|	031-8000-1107|	2020-03-01|	53000000|
|2020005|	양성태|	D0003|	팀원|	sungtae_yang@grep.com|	031-8000-1112|	2020-03-01|	53000000|

<br>

*HR_GRADE*
|EMP_NO|	YEAR|	HALF_YEAR|	SCORE|
|---|---|---|---|
|2017002|	2022|	1|	92|
|2018001|	2022|	1|	89|
|2019001|	2022|	1|	94|
|2020002|	2022|	1|	90|
|2020005|	2022|	1|	92|
|2017002|	2022|	2|	84|
|2018001|	2022|	2|	89|

<br>

**Sample Output**

|EMP_NO|	EMP_NAME|	GRADE|	BONUS|
|---|--|---|---|
|2017002|	정호식|	B|	6500000|
|2018001|	김민석|	B|	6000000|
|2019001|	김솜이|	B|	6000000|
|2020002|	김연주|	A|	7950000|
|2020005|	양성태|	B|	5300000|

<br>

### Solving

```sql
WITH GRADE2 AS (
    SELECT EMP_NO
         , CASE
                WHEN SUM(SCORE)/2 >= 96 THEN 'S'
                WHEN SUM(SCORE)/2 >= 90 THEN 'A'
                WHEN SUM(SCORE)/2 >= 80 THEN 'B'
                ELSE 'C'
            END AS GRADE
    FROM HR_GRADE
    GROUP BY EMP_NO
)

SELECT E.EMP_NO
     , E.EMP_NAME
     , G.GRADE
     , CASE 
            WHEN G.GRADE = 'S' THEN E.SAL*0.2
            WHEN G.GRADE = 'A' THEN E.SAL*0.15
            WHEN G.GRADE = 'B' THEN E.SAL*0.1
            ELSE E.SAL*0
        END AS BONUS
FROM GRADE2 G
 INNER JOIN HR_EMPLOYEES E ON G.EMP_NO = E.EMP_NO
ORDER BY EMP_NO
```
