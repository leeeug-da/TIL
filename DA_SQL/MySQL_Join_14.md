### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (JOIN) (있었는데요 없었습니다)
- *table* : ANIMAL_INS, ANIMAL_OUTS

**ANIMAL_INS**
|column|type|
|---|---|
|ANIMAL_ID|VARCHAR|
|ANIMAL_TYPE|VARCHAR|
|DATETIME|DATETIME|
|INTAKE_CONDITION|VARCHAR|
|NAME|VARCHAR|
|SEX_UPON_INTAKE|VARCHAR

`ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

**ANIMAL_OUTS**
|column|type|
|---|---|
|ANIMAL_ID|VARCHAR|
|ANIMAL_TYPE|VARCHAR|
|DATETIME|DATETIME|
|NAME|VARCHAR|
|SEX_UPON_OUTCOME|VARCHAR

`ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다. `ANIMAL_OUTS` 테이블의 `ANIMAL_ID`는 `ANIMAL_INS`의 `ANIMAL_ID`의 외래 키입니다.

<br>

### Problem 
관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일이 빠른 순으로 조회해야합니다.

<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A350276|	Cat|	2017-08-13 13:50:00|	Normal|	Jewel|	Spayed Female|
|A381217|	Dog|	2017-07-08 09:41:00|	Sick|	Cherokee|	Neutered Male|


*ANIMAL_OUTS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	NAME|	SEX_UPON_OUTCOME|
|---|---|---|---|---|
|A350276|	Cat|	2018-01-28 17:51:00|	Jewel|	Spayed Female|
|A381217|	Dog|	2017-06-09 18:51:00|	Cherokee|	Neutered Male|

**Sample Output**

|ANIMAL_ID|	NAME|
|---|---|
|A381217|	Cherokee|

<br>

### Solving

```sql
-- 보호 시작일보다 입양일이 더 빠른 동물 (AI.DATETIME < AO.DATETIME)
-- 아이디, 이름 
-- 보호 시작일이 빠른 순

SELECT AI.ANIMAL_ID
     , AI.NAME
FROM ANIMAL_INS AI
 JOIN ANIMAL_OUTS AO ON AI.ANIMAL_ID = AO.ANIMAL_ID
WHERE AI.DATETIME > AO.DATETIME
ORDER BY AI.DATETIME
```
