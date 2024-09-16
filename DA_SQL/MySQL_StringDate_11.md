### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (이름에 el이 들어가는 동물 찾기)
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
보호소에 돌아가신 할머니가 기르던 개를 찾는 사람이 찾아왔습니다. 이 사람이 말하길 할머니가 기르던 개는 이름에 'el'이 들어간다고 합니다. 동물 보호소에 들어온 동물 이름 중, 이름에 "EL"이 들어가는 개의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 이름 순으로 조회해주세요. 단, 이름의 대소문자는 구분하지 않습니다.



<br>

**Sample Input**

*ANIMAL_INS*
|ANIMAL_ID|	ANIMAL_TYPE|	DATETIME|	INTAKE_CONDITION|	NAME|	SEX_UPON_INTAKE|
|---|---|---|---|---|---|
|A355753	|Dog	|2015-09-10 13:14:00|	Normal|	Elijah|	Neutered Male|
|A352872	|Dog	|2015-07-09 17:51:00|	Aged|	Peanutbutter|	Neutered Male|
|A353259	|Dog	|2016-05-08 12:57:00|	Injured|	Bj|	Neutered Male|
|A373219	|Cat	|2014-07-29 11:43:00|	Normal|	Ella|	Spayed Female|
|A382192	|Dog	|2015-03-13 13:14:00|	Normal|	Maxwell 2|	Intact Male|
  
<br>

**Sample Output**

|ANIMAL_ID|	NAME|
|---|---|
|A355753|	Elijah|
|A382192|	Maxwell 2|

<br>

### Solving

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog'
  AND NAME LIKE '%EL%'
ORDER BY NAME
```
