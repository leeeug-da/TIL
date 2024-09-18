### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (오랜 기간 보호한 동물(2))
- *table* : ANIMAL_INS, ANIMAL_OUTS

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

**ANIMAL_OUTS**
|column|type|nullable|
|---|---|---|
|ANIMAL_ID|	VARCHAR(N)|	FALSE|
|ANIMAL_TYPE|	VARCHAR(N)|	FALSE|
|DATETIME|	DATETIME|	FALSE|
|NAME|	VARCHAR(N)|	TRUE|
|SEX_UPON_OUTCOME|	VARCHAR(N)|	FALSE|

`ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다. `ANIMAL_OUTS` 테이블의 `ANIMAL_ID`는 `ANIMAL_INS`의 `ANIMAL_ID`의 외래 키입니다.

### Problem
입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 기간이 긴 순으로 조회해야 합니다.



<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A354597|	Cat|	2014-05-02 12:16:00|	Normal|	Ariel|	Spayed Female|
|A362707|	Dog|	2016-01-27 12:27:00|	Sick|	Girly Girl|	Spayed Female|
|A370507|	Cat|	2014-10-27 14:43:00|	Normal|	Emily|	Spayed Female|
|A414513|	Dog|	2016-06-07 09:17:00|	Normal|	Rocky|	Neutered Male|
  
<br>

*ANIMAL_OUTS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	NAME|	SEX_UPON_OUTCOME|
|---|---|---|---|---|
|A354597|	Cat|	2014-06-03 12:30:00|	Ariel|	Spayed Female|
|A362707|	Dog|	2017-01-10 10:44:00|	Girly Girl|	Spayed Female|
|A370507|	Cat|	2015-08-15 09:24:00|	Emily|	Spayed Female|

**Sample Output**

|ANIMAL_ID|	NAME|
|---|---|
|A362707|	Girly Girl|
|A370507|	Emily|


<br>

### Solving

```sql
SELECT AO.ANIMAL_ID, AO.NAME
FROM ANIMAL_INS AI
 INNER JOIN ANIMAL_OUTS AO ON AI.ANIMAL_ID = AO.ANIMAL_ID 
ORDER BY DATEDIFF(AO.DATETIME, AI.DATETIME) DESC
LIMIT 2
```
