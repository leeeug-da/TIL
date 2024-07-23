### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (고양이와 개는 몇 마리 있을까)
- *table* : ANIMAL_INS

<br>

**ANIMAL_INS**
|column|type|nullable|
|---|---|---|
|ANIMAL_ID|	VARCHAR|	FALSE|
|ANIMAL_TYPE|	VARCHAR|	FALSE|
|DATETIME|	DATETIME|	FALSE|
|INTAKE_CONDITION|	VARCHAR|	FALSE|
|NAME|	VARCHAR|	TRUE|
|SEX_UPON_INTAKE|	VARCHAR|	FALSE|

`ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

<br>

### Problem 
동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회하는 SQL문을 작성해주세요. 이때 고양이를 개보다 먼저 조회해주세요.

<br>

**Sample Input**

*ANIMAL_INS*

|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A373219|	Cat|	2014-07-29| 11:43:00|	Normal|	Ella|	Spayed Female|
|A377750|	Dog|	2017-10-25| 17:17:00|	Normal|	Lucy|	Spayed Female|
|A354540|	Cat|	2014-12-11| 11:48:00|	Normal|	Tux|	Neutered Male|

<br>

**Sample Output**

|ANIMAL_TYPE|	count|
|---|---|
|Cat|	2|
|Dog|	1|

<br>

### Solving

```sql
SELECT ANIMAL_TYPE
     , COUNT(DISTINCT ANIMAL_ID) AS count
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE
```
