### Topic
- NULL
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (IS NULL) (
이름이 있는 동물의 아이디)
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
입양 게시판에 동물 정보를 게시하려 합니다. 동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 "No name"으로 표시해 주세요.

<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|--|---|---|---|
|A368930|	Dog|	2014-06-08| 13:20:00|	Normal|	Jewel|	Spayed Female|
|A524634|	Dog|	2015-01-02| 18:54:00|	Normal|	Meo|	Intact Female|
|A465637|	Dog|	2017-06-04| 08:17:00|	Injured|	NULL|	Neutered Male|

<br>

**Sample Output**

|ANIMAL_TYPE|	NAME|	SEX_UPON_INTAKE|
|---|---|---|
|Cat|	Jewel|	Spayed Female|
|Cat|	Meo|	Neutered Male|
|Dog|	No name|	Spayed Female|

<br>

### Solving

```sql
SELECT ANIMAL_TYPE
     , CASE
            WHEN NAME IS NULL THEN 'No name'
            ELSE NAME
        END AS NAME
     , SEX_UPON_INTAKE
FROM ANIMAL_INS
```
