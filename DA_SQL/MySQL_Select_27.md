### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (업그레이드 된 아이템 구하기)
- *table* : ITEM_INFO, ITEM_TREE

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

단, 각 아이템들은 오직 하나의 PARENT 아이템 ID를 가지며, ROOT 아이템의 PARENT 아이템 ID는 NULL 입니다. ROOT 아이템이 없는 경우는 존재하지 않습니다.

<br>

### Problem
아이템의 희귀도가 'RARE'인 아이템들의 모든 다음 업그레이드 아이템의 아이템 ID(ITEM_ID), 아이템 명(ITEM_NAME), 아이템의 희귀도(RARITY)를 출력하는 SQL 문을 작성해 주세요. 이때 결과는 아이템 ID를 기준으로 내림차순 정렬주세요.

<br>

**Sample Input**

*ITEM_INFO*
|ITEM_ID|	ITEM_NAME|	RARITY|	PRICE|
|---|---|---|---|
|0|	ITEM_A|	RARE|	10000|
|1|	ITEM_B|	RARE|	9000|
|2|	ITEM_C|	LEGEND|	11000|
|3|	ITEM_D|	RARE|	10000|
|4|	ITEM_E|	RARE|	12000|

<br>

*ITEM_TREE*
|ITEM_ID|	PARENT_ITEM_ID|
|---|---|
|0|	NULL|
|1|	0|
|2|	0|
|3|	1|
|4|	1|

<br>

**Sample Output**
|ITEM_ID|	ITEM_NAME|	RARITY|
|---|---|---|
|4|	ITEM_E|	RARE|
|3|	ITEM_D|	RARE|
|2|	ITEM_C|	LEGEND|
|1|	ITEM_B|	RARE|

<br>

### Solving

```sql
SELECT II.ITEM_ID, II.ITEM_NAME, II.RARITY
FROM ITEM_INFO II
 JOIN ITEM_TREE IT ON II.ITEM_ID = IT.ITEM_ID
WHERE IT.PARENT_ITEM_ID IN (SELECT ITEM_ID
                            FROM ITEM_INFO
                            WHERE RARITY = 'RARE')
ORDER BY ITEM_ID DESC
```
