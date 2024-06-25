### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (보호소에서 중성화한 동물)
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

### Problem 
보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화1되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.



**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A367438|	Dog|	2015-09-10 16:01:00|	Normal|	Cookie|	Spayed Female|
|A382192|	Dog|	2015-03-13 13:14:00|	Normal|	Maxwell 2|	Intact Male|
|A405494|	Dog|	2014-05-16 14:17:00|	Normal|	Kaila|	Spayed Female|
|A410330|	Dog|	2016-09-11 14:09:00|	Sick|	Chewy|	Intact Female|

*ANIMAL_OUTS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	NAME|	SEX_UPON_OUTCOME|
|---|---|---|---|---|
|A367438|	Dog|	2015-09-12 13:30:00|	Cookie|	Spayed Female|
|A382192|	Dog|	2015-03-16 13:46:00|	Maxwell 2|	Neutered Male|
|A405494|	Dog|	2014-05-20 11:44:00|	Kaila|	Spayed Female|
|A410330|	Dog|	2016-09-13 13:46:00|	Chewy|	Spayed Female|

<br>

**Sample Output**
|ANIMAL_ID|	ANIMAL_TYPE|	NAME|
|---|---|---|
|A382192|	Dog|	Maxwell 2|
|A410330|	Dog|	Chewy|


<br>

### Solving
```sql
-- 보호소에 들어올 당시에는 중성화 X (ANIMAL_INS: SEX_UPON_INTAKE = Intact)
-- 보호소를 나갈 당시에는 중성화 O (ANIMAL_OUTS: SEX_UPON_OUTCOME = Spayed or Neutered)
-- 아이디, 생물 종, 이름
-- 아이디 순으로 조회

SELECT ANIMAL_ID
     , ANIMAL_TYPE
     , NAME
FROM ANIMAL_INS 
WHERE SEX_UPON_INTAKE LIKE 'Intact%'
  AND ANIMAL_ID IN (SELECT ANIMAL_ID
                      FROM ANIMAL_OUTS 
                    WHERE SEX_UPON_OUTCOME LIKE 'Spayed%' 
                       OR SEX_UPON_OUTCOME LIKE 'Neutered%')
```
