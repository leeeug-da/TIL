### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (모든 레코드 조회하기)
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
동물 보호소에 들어온 모든 동물의 정보를 ANIMAL_ID순으로 조회하는 SQL문을 작성해주세요. 

<br>

**Sample Output**

|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A349996|	Cat|	2018-01-22 14:32:00|	Normal|	Sugar|	Neutered Male|
|A350276|	Cat|	2017-08-13 13:50:00|	Normal|	Jewel|	Spayed Female|
|A350375|	Cat|	2017-03-06 15:01:00|	Normal|	Meo|	Neutered Male|
|A352555|	Dog|	2014-08-08 04:20:00|	Normal|	Harley|	Spayed Female|

<br>

### Solving

```sql
SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID                  
```
