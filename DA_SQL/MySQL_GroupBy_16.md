### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
조건에 맞는 사원 정보 조회하기)
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


`HR_EMPLOYEES` 테이블의 구조는 다음과 같으며 `EMP_NO`, `EMP_NAME`, `DEPT_ID`, `POSITION`, `EMAIL`, `COMP_TEL`, `HIRE_DATE`, `SAL`은 각각 사번, 성명, 부서 ID, 직책, 이메일, 전화번호, 입사일, 연봉을 의미합니다.

<br>

**HR_GRADE**
|column|type|nullable|
|---|---|---|
|EMP_NO|	VARCHAR|	FALSE|
|YEAR|	NUMBER|	FALSE|
|HALF_YEAR|	NUMBER|	FALSE|
|SCORE|	NUMBER|	FALSE|

`HR_GRADE`의 구조는 다음과 같으며 `EMP_NO`, `YEAR`, `HALF_YEAR`, `SCORE`는 각각 사번, 연도, 반기, 평가 점수를 의미합니다.

<br>

### Problem
`HR_EMPLOYEES`, `HR_GRADE` 테이블에서 2022년도 한해 평가 점수가 가장 높은 사원 정보를 조회하려 합니다. 2022년도 평가 점수가 가장 높은 사원들의 점수, 사번, 성명, 직책, 이메일을 조회하는 SQL문을 작성해주세요.

2022년도의 평가 점수는 상,하반기 점수의 합을 의미하고, 평가 점수를 나타내는 컬럼의 이름은 `SCORE`로 해주세요.



<br>

**Sample Input**

*HR_EMPLOYEES*
|EMP_NO|	EMP_NAME|	DEPT_ID|	POSITION|	EMAIL|	COMP_TEL|	HIRE_DATE|	SAL|
|---|---|---|---|---|---|---|---|
|2017002|	정호식|	D0001|	팀장|	hosick_jung@grepp.com|	031-8000-1101|	2017-03-01|	65000000|
|2018001|	김민석|	D0001|	팀원|	minseock_kim@grepp.com|	031-8000-1102|	2018-03-01|	60000000|
|2019001|	김솜이|	D0002|	팀장|	somi_kim@grepp.com|	031-8000-1106|	2019-03-01|	60000000|
|2020002|	김연주|	D0002|	팀원|	yeonjoo_kim@grepp.com|	031-8000-1107|	2020-03-01|	53000000|


*HR_GRADE*
|MP_NO|	YEAR|	HALF_YEAR|	SCORE|
|---|---|---|---|
|2017002|	2022|	1|	92|
|2018001|	2022|	1|	89|
|2019001|	2022|	1|	94|
|2020002|	2022|	1|	90|
|2020005|	2022|	1|	92|
|2017002|	2022|	2|	84|

<br>

**Sample Output**

|SCORE|	EMP_NO|	EMP_NAME|	POSITION|	EMAIL|
|---|---|---|---|---|
|181|	202002|	김연주|	팀원|	yeonjoo_kim@grepp.com|

<br>

### Solving

```sql
WITH SCORE AS (
    SELECT EMP_NO
         , SUM(SCORE) SCORE
    FROM HR_GRADE
    WHERE YEAR = 2022
    GROUP BY EMP_NO
)
SELECT S.SCORE
     , S.EMP_NO
     , E.EMP_NAME
     , E.POSITION
     , E.EMAIL
FROM HR_EMPLOYEES E
 JOIN SCORE S ON E.EMP_NO = S.EMP_NO
ORDER BY SCORE DESC
LIMIT 1
```
