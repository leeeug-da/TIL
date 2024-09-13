### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (루시와 엘라 찾기)
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
동물 보호소에 들어온 동물 중 이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물의 아이디와 이름, 성별 및 중성화 여부를 조회하는 SQL 문을 작성해주세요. 이때 결과는 아이디 순으로 조회해주세요.



<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A373219|	Cat|	2014-07-29| 11:43:00|	Normal|	Ella|	Spayed Female|
|A377750|	Dog|	2017-10-25| 17:17:00|	Normal|	Lucy|	Spayed Female|
|A353259|	Dog|	2016-05-08| 12:57:00|	Injured|	Bj|	Neutered Male|
|A354540|	Cat|	2014-12-11| 11:48:00|	Normal|	Tux|	Neutered Male|
|A354597|	Cat|	2014-05-02| 12:16:00|	Normal|	Ariel|	Spayed Female|
  
<br>

**Sample Output**

|ANIMAL_ID|	NAME|	SEX_UPON_INTAKE|
|---|---|---|
|A373219|	Ella|	Spayed Female|
|A377750|	Lucy|	Spayed Female|

<br>

### Solving

```sql
SELECT ANIMAL_ID, NAME , SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
ORDER BY ANIMAL_ID
```
