### Topic
- Bitwise Operator
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (FrontEnd 개발자 찾기)
- *table* : SKILLCODES, DEVELOPERS

**SKILLCODES**
|column|type|
|---|---|
|NAME|VARCHAR|
|CATEGORY|VARCHAR|
|CODE|INTEGER|

`SKILLCODES` 테이블의 구조는 다음과 같으며, `NAME`, `CATEGORY`, `CODE`는 각각 스킬의 이름, 스킬의 범주, 스킬의 코드를 의미합니다. 스킬의 코드는 2진수로 표현했을 때 각 bit로 구분될 수 있도록 2의 제곱수로 구성되어 있습니다.

**DEVELOPERS**
|column|type|
|---|---|
|ID|VARCHAR|
|FIRST_NAME|VARCHAR|
|LAST_NAME|VARCHAR|
|EMAIL|VARCHAR|
|SKILL_CODE|INTEGER

`DEVELOPERS` 테이블은 개발자들의 프로그래밍 스킬 정보를 담은 테이블입니다. `DEVELOPERS` 테이블의 구조는 다음과 같으며, `ID`, `FIRST_NAME`, `LAST_NAME`, `EMAIL`, `SKILL_CODE`는 각각 개발자의 ID, 이름, 성, 이메일, 스킬 코드를 의미합니다. `SKILL_CODE` 컬럼은 INTEGER 타입이고, 2진수로 표현했을 때 각 bit는 `SKILLCODES` 테이블의 코드를 의미합니다.

예를 들어 어떤 개발자의 `SKILL_CODE`가 400 (=b'110010000')이라면, 이는 `SKILLCODES` 테이블에서 CODE가 256 (=b'100000000'), 128 (=b'10000000'), 16 (=b'10000') 에 해당하는 스킬을 가졌다는 것을 의미합니다.

### Problem 
`DEVELOPERS` 테이블에서 Front End 스킬을 가진 개발자의 정보를 조회하려 합니다. 조건에 맞는 개발자의 ID, 이메일, 이름, 성을 조회하는 SQL 문을 작성해 주세요.

결과는 ID를 기준으로 오름차순 정렬해 주세요.



**Sample Input**

*SKILLCODES*
|NAME|	CATEGORY|	CODE|
|---|---|---|
|C++|	Back End|	4|
|JavaScript|	Front End|	16|
|Java|	Back End|	128|
|Python|	Back End|	256|
|C#|	Back End|	1024|
|React|	Front End|	2048|
|Vue|	Front End|	8192|
|Node.js|	Back End|	16384|

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
|ID|	EMAIL|	FIRST_NAME|	LAST_NAME|
|---|---|---|---|
|D161|	carsen_garza@grepp.co|	Carsen	|Garza|
|D162|	cade_cunningham@grepp.co|	Cade|	Cunningham|
|D165|	jerami_edwards@grepp.co|	Jerami|	Edwards|



<br>

### Solving
```sql
-- Front End 스킬을 가진 개발자의 정보
-- ID, EMAIL, FIRST_NAME, LAST_NAME
-- ID ASC

SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPERS 
WHERE SKILL_CODE & (
                     SELECT SUM(CODE)
                     FROM SKILLCODES
                     WHERE CATEGORY = 'Front End'
                    )
ORDER BY ID
```
