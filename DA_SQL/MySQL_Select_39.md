### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (언어별 개발자 분류하기)
- *table* : SKILLCODES, DEVELOPERS

<br>

**SKILLCODES**
|column|type|nullable|
|---|---|---|
|NAME|	VARCHAR(N)|	Y|	
|CATEGORY|	VARCHAR(N)|	N|	
|CODE|	INTEGER|	Y|

`SKILLCODES` 테이블의 구조는 다음과 같으며, `NAME`, `CATEGORY`, `CODE`는 각각 스킬의 이름, 스킬의 범주, 스킬의 코드를 의미합니다. 스킬의 코드는 2진수로 표현했을 때 각 bit로 구분될 수 있도록 2의 제곱수로 구성되어 있습니다.

<br>

**DEVELOPERS**
|column|type|nullable|
|---|---|---|
|ID|	VARCHAR(N)|		N|
|FIRST_NAME|	VARCHAR(N)|	Y|
|LAST_NAME|	VARCHAR(N)|		Y|
|EMAIL|	VARCHAR(N)|		N|
|SKILL_CODE|	INTEGER|		N|


`DEVELOPERS` 테이블의 구조는 다음과 같으며, `ID`, `FIRST_NAME`, `LAST_NAME`, `EMAIL`, `SKILL_CODE`는 각각 개발자의 ID, 이름, 성, 이메일, 스킬 코드를 의미합니다. `SKILL_CODE` 컬럼은 INTEGER 타입이고, 2진수로 표현했을 때 각 bit는 `SKILLCODES` 테이블의 코드를 의미합니다.

<br>

### Problem
`DEVELOPERS` 테이블에서 GRADE별 개발자의 정보를 조회하려 합니다. GRADE는 다음과 같이 정해집니다.

- A : Front End 스킬과 Python 스킬을 함께 가지고 있는 개발자
- B : C# 스킬을 가진 개발자
- C : 그 외의 Front End 개발자

GRADE가 존재하는 개발자의 GRADE, ID, EMAIL을 조회하는 SQL 문을 작성해 주세요.

결과는 GRADE와 ID를 기준으로 오름차순 정렬해 주세요.

<br>

**Sample Input**

*SKILLCODES*
|NAME|	CATEGORY|	CODE|
|---|---|---|
|C++	|Back End|	4|
|JavaScript	|Front End|	16|
|Java	|Back End|	128|
|Python	|Back End|	256|
|C#	|Back End|	1024|
|React	|Front End|	2048|
|Vue	|Front End|	8192|
|Node.js|	Back End|	16384|

<br>

*DEVELOPERS*
|ID|	FIRST_NAME|	LAST_NAME|	EMAIL|	SKILL_CODE|
|---|---|---|---|---|
|D165|	Jerami|	Edwards|	jerami_edwards@grepp.co|	400|
|D161|	Carsen|	Garza|	carsen_garza@grepp.co|	2048|
|D164|	Kelly|	Grant|	kelly_grant@grepp.co|	1024|
|D163|	Luka|	Cory|	luka_cory@grepp.co|	16384|
|D162|	Cade|	Cunningham|	cade_cunningham@grepp.co|	8452|

<br>

**Sample Output**
|GRADE|	ID|	EMAIL|
|---|---|---|
|A|	D162|	cade_cunningham@grepp.co|
|A|	D165|	jerami_edwards@grepp.co|
|B|	D164|	kelly_grant@grepp.co|
|C|	D161|	carsen_garza@grepp.co|

<br>

### Solving

```sql
WITH GRADES AS (
    SELECT ID
         , EMAIL
         , CASE
               WHEN COUNT(CASE WHEN CATEGORY = 'Front End' THEN 1 END) > 0 AND 
                    COUNT(CASE WHEN NAME = 'Python' THEN 1 END) > 0 
                    THEN 3
               WHEN COUNT(CASE WHEN NAME = 'C#' THEN 1 END) > 0 THEN 2
               WHEN COUNT(CASE WHEN CATEGORY = 'Front End' THEN 1 END) > 0 THEN 1
           END AS SCORE
    FROM DEVELOPERS AS D
    JOIN SKILLCODES AS S ON D.SKILL_CODE & S.CODE
    GROUP BY ID,EMAIL
    HAVING SCORE > 0
)

SELECT CASE 
            WHEN SCORE = 3 THEN 'A'
            WHEN SCORE = 2 THEN 'B'
            WHEN SCORE = 1 THEN 'C'
       END AS GRADE
     , ID
     , EMAIL
FROM GRADES
ORDER BY GRADE, ID
```
