### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (중성화 여부 파악하기)
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
보호소의 동물이 중성화되었는지 아닌지 파악하려 합니다. 중성화된 동물은 SEX_UPON_INTAKE 컬럼에 'Neutered' 또는 'Spayed'라는 단어가 들어있습니다. 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시해주세요.



<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A355753	|Dog	|2015-09-10 13:14:00|	Normal|	Elijah|	Neutered Male|
|A373219	|Cat	|2014-07-29 11:43:00|	Normal|	Ella|	Spayed Female|
|A382192	|Dog	|2015-03-13 13:14:00|	Normal|	Maxwell 2|	Intact Male|
  
<br>

**Sample Output**

|ANIMAL_ID|	NAME|	중성화|
|---|---|---|
|A355753|	Elijah|	O|
|A373219|	Ella|	O|
|A382192|	Maxwell 2|	X|

<br>

### Solving

```sql
SELECT ANIMAL_ID
     , NAME
     , CASE
            WHEN SEX_UPON_INTAKE LIKE 'Neutered%' THEN 'O'
            WHEN SEX_UPON_INTAKE LIKE 'Spayed%' THEN 'O'
            ELSE 'X'
        END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```
