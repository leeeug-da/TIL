### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (
부서별 평균 연봉 조회하기)
- *table* : HR_DEPARTMENT, HR_EMPLOYEES

<br>

**HR_DEPARTMENT**
|column|type|nullable|
|---|---|---|
|DEPT_ID|	VARCHAR|	FALSE|
|DEPT_NAME_KR|	VARCHAR|	FALSE|
|DEPT_NAME_EN|	VARCHAR|	FALSE|
|LOCATION|	VARCHAR|	FALSE|

`HR_DEPARTMENT` 테이블의 구조는 다음과 같으며 `DEPT_ID`, `DEPT_NAME_KR`, `DEPT_NAME_EN`, `LOCATION`은 각각 부서 ID, 국문 부서명, 영문 부서명, 부서 위치를 의미합니다.

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

### Problem
`HR_DEPARTMENT`와 `HR_EMPLOYEES` 테이블을 이용해 부서별 평균 연봉을 조회하려 합니다. 부서별로 부서 ID, 영문 부서명, 평균 연봉을 조회하는 SQL문을 작성해주세요.

평균연봉은 소수점 첫째 자리에서 반올림하고 컬럼명은 `AVG_SAL`로 해주세요.
결과는 부서별 평균 연봉을 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*HR_DEPARTMENT*
|DEPT_ID|	DEPT_NAME_KR|	DEPT_NAME_EN|	LOCATION|
|---|---|---|---|
|D0005|	재무팀|	Finance|	그렙타워 5층|
|D0006|	구매팀|	Purchasing|	그렙타워 5층|
|D0007|	마케팅팀|	Marketing|	그렙타워 6층|

*HR_EMPLOYEES*
|EMP_NO|	EMP_NAME|	DEPT_ID|	POSITION|	EMAIL|	COMP_TEL|	HIRE_DATE|	SAL|
|---|---|---|---|---|---|---|---|
|2017002|	정호식|	D0001|	팀장|	hosick_jung@grepp.com|	031-8000-1101|	2017-03-01|	65000000|
|2018001|	김민석|	D0001|	팀원|	minseock_kim@grepp.com|	031-8000-1102|	2018-03-01|	60000000|
|2019001|	김솜이|	D0002|	팀장|	somi_kim@grepp.com|	031-8000-1106|	2019-03-01|	60000000|
|2020002|	김연주|	D0002|	팀원|	yeonjoo_kim@grepp.com|	031-8000-1107|	2020-03-01|	53000000|

<br>

**Sample Output**

|DEPT_ID|	DEPT_NAME_EN|	AVG_SAL|
|---|---|---|
|D0007|	Marketing|	54666667|
|D0006|	Purchasing|	54250000|
|D0005|	Finance|	52000000|

<br>

### Solving

```sql
WITH DEPT_SAL AS (
    SELECT DEPT_ID
         , ROUND(AVG(SAL)) AS AVG_SAL
    FROM HR_EMPLOYEES
    GROUP BY DEPT_ID
)

SELECT S.DEPT_ID
     , D.DEPT_NAME_EN
     , S.AVG_SAL
FROM DEPT_SAL S 
 JOIN HR_DEPARTMENT D ON S.DEPT_ID = D.DEPT_ID
ORDER BY AVG_SAL DESC
```
