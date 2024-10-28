### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (Python 개발자 찾기)
- *table* : DEVELOPER_INFOS

<br>

**DEVELOPER_INFOS**
|column|type|nullable|
|---|---|---|
|ID|	VARCHAR(N)|		N|
|FIRST_NAME|	VARCHAR(N)|		Y|
|LAST_NAME|	VARCHAR(N)|		Y|
|EMAIL|	VARCHAR(N)|	N|
|SKILL_1|	VARCHAR(N)|	Y|
|SKILL_2|	VARCHAR(N)|	Y|
|SKILL_3|	VARCHAR(N)|	Y|

`ITEM_INFO` 테이블은 다음과 같으며, `ITEM_ID`, `ITEM_NAME`, `RARITY`, `PRICE`는 각각 아이템 ID, 아이템 명, 아이템의 희귀도, 아이템의 가격을 나타냅니다.

<br>

### Problem
`DEVELOPER_INFOS` 테이블에서 Python 스킬을 가진 개발자의 정보를 조회하려 합니다. Python 스킬을 가진 개발자의 ID, 이메일, 이름, 성을 조회하는 SQL 문을 작성해 주세요.

결과는 ID를 기준으로 오름차순 정렬해 주세요.

<br>

**Sample Input**

*DEVELOPER_INFOS*
|ID|	FIRST_NAME|	LAST_NAME|	EMAIL|	SKILL_1|	SKILL_2|	SKILL_3|
|---|---|---|---|---|---|---|
|D165|	Jerami|	Edwards|	jerami_edwards@grepp.co|	Java|	JavaScript|	Python|
|D161|	Carsen|	Garza|	carsen_garza@grepp.co|	React|		| |
|D164|	Kelly|	Grant|	kelly_grant@grepp.co|	C#|		| |
|D163|	Luka|	Cory|	luka_cory@grepp.co|	Node.js|		| |
|D162|	Cade|	Cunningham|	cade_cunningham@grepp.co|	Vue|	C++|	Python|

<br>

**Sample Output**
|ID|	EMAIL|	FIRST_NAME|	LAST_NAME|
|---|---|---|---|
|D162|	cade_cunningham@grepp.co|	Cade|	Cunningham|
|D165|	jerami_edwards@grepp.co|	Jerami|	Edwards|

<br>

### Solving

```sql
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE SKILL_1 = 'Python'
  OR SKILL_2 = 'Python'
  OR SKILL_3 = 'Python'
ORDER BY ID 
```
