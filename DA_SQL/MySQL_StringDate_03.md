### Topic
- String, Date
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (String, Date) (조건에 부합하는 중고거래 상태 조회하기)
- *table* : USED_GOODS_BOARD

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

`USED_GOODS_BOARD` 테이블은 다음과 같으며 `BOARD_ID`, `WRITER_ID`, `TITLE`, `CONTENTS`, `PRICE`, `CREATED_DATE`, `STATUS`, `VIEWS`은 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

<br>

### Problem
`USED_GOODS_BOARD` 테이블에서 2022년 10월 5일에 등록된 중고거래 게시물의 게시글 ID, 작성자 ID, 게시글 제목, 가격, 거래상태를 조회하는 SQL문을 작성해주세요. 거래상태가 SALE 이면 판매중, RESERVED이면 예약중, DONE이면 거래완료 분류하여 출력해주시고, 결과는 게시글 ID를 기준으로 내림차순 정렬해주세요.

<br>

**Sample Input**

*USED_GOODS_BOARD*
|BOARD_ID|	WRITER_ID|	TITLE|	CONTENTS|	PRICE|	CREATED_DATE|	STATUS|	VIEWS|
|---|---|---|---|---|---|---|---|
|B0001|	kwag98|	반려견 배변패드 팝니다|	정말 저렴히 판매합니다. 전부 미개봉 새상품입니다.|	12000|	2022-10-01|	DONE|	250|
|B0002|	lee871201|	국내산 볶음참깨|	직접 농사지은 참깨입니다.|	3000|	2022-10-02|	DONE|	121|
|B0003|	goung12|	배드민턴 라켓|	사놓고 방치만 해서 팝니다.|	9000|	2022-10-02|	SALE|	212|
|B0004|	keel1990|	디올 귀걸이|	신세계강남점에서 구입. 정품 아닐시 백퍼센트 환불|	130000|	2022-10-02|	SALE|	199|
|B0005|	haphli01|	스팸클래식 팔아요|	유통기한 2025년까지에요|	10000|	2022-10-02|	SALE|	121|

<br>

**Sample Output**

|BOARD_ID|	WRITER_ID|	TITLE|	PRICE|	STATUS|
|---|---|---|---|---|
|B0010|	keel1990|	철제선반5단|	10000|	판매중|
|B0009|	yawoong67|	선반 팝니다|	12000|	거래완료|

<br>

### Solving

```sql
SELECT BOARD_ID, WRITER_ID, TITLE, PRICE
       , CASE 
            WHEN STATUS = 'SALE' THEN '판매중'
            WHEN STATUS = 'RESERVED' THEN '예약중'
            ELSE '거래완료'
         END AS STATUS
FROM USED_GOODS_BOARD
WHERE CREATED_DATE = '2022-10-05'
ORDER BY BOARD_ID DESC
```
