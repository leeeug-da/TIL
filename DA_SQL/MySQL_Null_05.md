### Topic
- NULL
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (IS NULL) (
ROOT 아이템 구하기)
- *table* : ITEM_INFO, ITEM_TREE

<br>

어느 한 게임에서 사용되는 아이템들은 업그레이드가 가능합니다.
'ITEM_A'->'ITEM_B'와 같이 업그레이드가 가능할 때
'ITEM_A'를 'ITEM_B'의 PARENT 아이템,
PARENT 아이템이 없는 아이템을 ROOT 아이템이라고 합니다.

예를 들어 'ITEM_A'->'ITEM_B'->'ITEM_C' 와 같이 업그레이드가 가능한 아이템이 있다면
'ITEM_C'의 PARENT 아이템은 'ITEM_B'
'ITEM_B'의 PARENT 아이템은 'ITEM_A'
ROOT 아이템은 'ITEM_A'가 됩니다.

<br>

**ITEM_INFO**
|column|type|nullable|
|---|---|---|
|ITEM_ID|	INTEGER|	FALSE|
|ITEM_NAME|	VARCHAR(N)|	FALSE|
|RARITY|	INTEGER|	FALSE|
|PRICE|	INTEGER|	FALSE|

`ITEM_INFO` 테이블은 다음과 같으며, `ITEM_ID`, `ITEM_NAME`, `RARITY`, `PRICE`는 각각 아이템 ID, 아이템 명, 아이템의 희귀도, 아이템의 가격을 나타냅니다.

<br>

**ITEM_TREE**
|column|type|nullable|
|---|---|---|
|ITEM_ID|	INTEGER|	FALSE|
|PARENT_ITEM_ID|	INTEGER|	TRUE|

`ITEM_TREE` 테이블은 다음과 같으며, `ITEM_ID`, `PARENT_ITEM_ID`는 각각 아이템 ID, PARENT 아이템의 ID를 나타냅니다.

단, 각 아이템들은 오직 하나의 PARENT 아이템 ID를 가지며, ROOT 아이템의 PARENT 아이템 ID는 NULL 입니다.

ROOT 아이템이 없는 경우는 존재하지 않습니다.

<br>

### Problem
ROOT 아이템을 찾아 아이템 ID(ITEM_ID), 아이템 명(ITEM_NAME)을 출력하는 SQL문을 작성해 주세요. 이때, 결과는 아이템 ID를 기준으로 오름차순 정렬해 주세요.

<br>

**Sample Input**

*ITEM_INFO*
|ITEM_ID|	ITEM_NAME|	RARITY|	PRICE|
|---|---|---|---|
|0|	ITEM_A|	COMMON|	10000|
|1|	ITEM_B|	LEGEND|	9000|
|2|	ITEM_C|	LEGEND|	11000|
|3|	ITEM_D|	UNIQUE|	10000|
|4|	ITEM_E|	LEGEND|	12000|

<br>

*ITEM_INFO*
|ITEM_ID|	PARENT_ITEM_ID|
|---|---|
|0|	NULL|
|1|	0|
|2|	0|
|3|	NULL|
|4|	3|

<br>

**Sample Output**

|ITEM_ID|	ITEM_NAME|
|---|---|
|0|	ITEM_A|
|3|	ITEM_D|

<br>

### Solving

```sql
SELECT ITEM_ID
     , ITEM_NAME
FROM ITEM_INFO
WHERE ITEM_ID IN (SELECT ITEM_ID
                  FROM ITEM_TREE
                  WHERE PARENT_ITEM_ID IS NULL)
ORDER BY ITEM_ID
```
