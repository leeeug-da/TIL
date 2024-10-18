### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (어린 동물 찾기)
- *table* : ANIMAL_INS

<br>

**ANIMAL_INS**
|column|type|nullable|
|---|---|---|
|ANIMAL_ID|	VARCHAR(N)|	FALSE|
|ANIMAL_TYPE|	VARCHAR(N)|	FALSE|
|DATETIME|	DATETIME|	FALSE|
|INTAKE_CONDITION|	VARCHAR(N)|	FALSE|
|NAME|	VARCHAR(N)|	TRUE|
|SEX_UPON_INTAKE|	VARCHAR(N)|	FALSE|

`ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

<br>

### Problem
동물 보호소에 들어온 동물 중 젊은 동물1의 아이디와 이름을 조회하는 SQL 문을 작성해주세요. 이때 결과는 아이디 순으로 조회해주세요.

<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A365172|	Dog|	2014-08-26 12:53:00|	Normal|	Diablo|	Neutered Male|
|A367012|	Dog|	2015-09-16 09:06:00|	Sick|	Miller|	Neutered Male|
|A365302|	Dog|	2017-01-08 16:34:00|	Aged|	Minnie|	Spayed Female|
|A381217|	Dog|	2017-07-08 09:41:00|	Sick|	Cherokee|	Neutered Male|

<br>

**Sample Output**
|ANIMAL_ID|	NAME|
|---|---|
|A365172|	Diablo|
|A367012|	Miller|
|A381217|	Cherokee|


<br>

### Solving

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID     
```
