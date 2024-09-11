### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (조건에 맞는 사용자 정보 조회하기)
- *table* : USED_GOODS_BOARD, USED_GOODS_USER

<br>

**USED_GOODS_BOARD**
|column|type|nullable|
|---|---|---|
|BOARD_ID|	VARCHAR(5)|	FALSE|
|WRITER_ID|	VARCHAR(50)|	FALSE|
|TITLE|	VARCHAR(100)|	FALSE|
|CONTENTS|	VARCHAR(1000)|	FALSE|
|PRICE|	NUMBER|	FALSE|
|CREATED_DATE|	DATE|	FALSE|
|STATUS|	VARCHAR(10)|	FALSE|
|VIEWS|	NUMBER|	FALSE|

`USED_GOODS_BOARD` 테이블은 다음과 같으며 `BOARD_ID`, `WRITER_ID`, `TITLE`, `CONTENTS`, `PRICE`, `CREATED_DATE`, `STATUS`, `VIEWS`는 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

<br>

**USED_GOODS_USER**
|column|type|nullable|
|---|---|---|
|USER_ID|	VARCHAR(50)|	FALSE|
|NICKANME|	VARCHAR(100)|	FALSE|
|CITY|	VARCHAR(100)|	FALSE|
|STREET_ADDRESS1|	VARCHAR(100)|	FALSE|
|STREET_ADDRESS2|	VARCHAR(100)|	TRUE|
|TLNO|	VARCHAR(20)|	FALSE|

`USED_GOODS_USER` 테이블은 다음과 같으며 `USER_ID`, `NICKNAME`, `CITY`, `STREET_ADDRESS1`, `STREET_ADDRESS2`, `TLNO`는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 의미합니다.

<br>

### Problem
`USED_GOODS_BOARD`와 `USED_GOODS_USER` 테이블에서 중고 거래 게시물을 3건 이상 등록한 사용자의 사용자 ID, 닉네임, 전체주소, 전화번호를 조회하는 SQL문을 작성해주세요. 이때, 전체 주소는 시, 도로명 주소, 상세 주소가 함께 출력되도록 해주시고, 전화번호의 경우 xxx-xxxx-xxxx 같은 형태로 하이픈 문자열(-)을 삽입하여 출력해주세요. 결과는 회원 ID를 기준으로 내림차순 정렬해주세요.



<br>

**Sample Input**

*USED_GOODS_BOARD*
|BOARD_ID|	WRITER_ID|	TITLE|	CONTENTS|	PRICE|	CREATED_DATE|	STATUS|	VIEWS|
|---|---|---|---|---|---|---|---|
|B0001|	dhfkzmf09|	칼라거펠트 코트|	양모 70%이상 코트입니다.|	120000|	2022-10-14|	DONE|	104|
|B0002|	lee871201|	국내산 볶음참깨|	직접 농사지은 참깨입니다.|	3000|	2022-10-02|	DONE|	121|
|B0003|	dhfkzmf09|	나이키 숏패팅|	사이즈는 M입니다.|	40000|	2022-10-17|	DONE|	98|
|B0004|	kwag98|	반려견 배변패드 팝니다|	정말 저렴히 판매합니다. 전부 미개봉 새상품입니다.|	12000|	2022-10-01|	DONE|	250|
|B0005|	dhfkzmf09|	PS4|	PS5 구매로인해 팝니다.|	250000|	2022-11-03|	DONE|	111|
  
<br>

*USED_GOODS_USER*
|USER_ID|	NICKNAME|	CITY|	STREET_ADDRESS1|	STREET_ADDRESS2|	TLNO|
|---|---|---|---|---|---|
|dhfkzmf09|	찐찐|	성남시|	분당구 수내로 13|	A동 1107호|	01053422914|
|dlPcks90|	썹썹|	성남시|	분당구 수내로 74|	401호|	01034573944|
|cjfwls91|	점심만금식|	성남시|	분당구 내정로 185|	501호|	01036344964|
|dlfghks94|	희망|	성남시|	분당구 내정로 101|	203동 102호|	01032634154|
|rkdhs95|	용기|	성남시|	분당구 수내로 23|	501호|	01074564564|

<br>

**Sample Output**

|USER_ID|	NICKNAME|	전체주소|	전화번호|
|---|---|---|---|
|dhfkzmf09|	찐찐|	성남시 분당구 수내로 13 A동 1107호|	010-5342-2914|

<br>

### Solving

```sql
SELECT USER_ID
     , NICKNAME
     , CONCAT(CITY, ' ', STREET_ADDRESS1, ' ', STREET_ADDRESS2) AS 전체주소
     , CONCAT(SUBSTRING(TLNO, 1, 3), '-',
              SUBSTRING(TLNO, 4, 4), '-',
              SUBSTRING(TLNO, 8, 4)) AS 전화번호
FROM USED_GOODS_USER
WHERE USER_ID IN (SELECT WRITER_ID AS USER_ID
                  FROM USED_GOODS_BOARD
                  GROUP BY WRITER_ID
                  HAVING COUNT(BOARD_ID) >= 3
                  )
ORDER BY USER_ID DESC
```
