### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (조건에 맞는 사용자와 총 거래금액 조회하기)
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

`USED_GOODS_USER` 테이블은 다음과 같으며 `USER_ID`, `NICKNAME`, `CITY`, `STREET_ADDRESS1`, `STREET_ADDRESS2`, `TLNO`는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 를 의미합니다.

<br>

### Problem
`USED_GOODS_BOARD`와 `USED_GOODS_USER` 테이블에서 완료된 중고 거래의 총금액이 70만 원 이상인 사람의 회원 ID, 닉네임, 총거래금액을 조회하는 SQL문을 작성해주세요. 결과는 총거래금액을 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*USED_GOODS_BOARD*
|BOARD_ID|	WRITER_ID|	TITLE|	CONTENTS|	PRICE|	CREATED_DATE|	STATUS|	VIEWS|
|---|---|---|---|---|---|---|---|
|B0001|	zkzkdh1|	캠핑의자|	가벼워요 깨끗한 상태입니다. 2개|	25000|	2022-11-29|	SALE|	34|
|B0002|	miyeon89|	벽걸이 에어컨|	엘지 휘센 7평|	100000|	2022-11-29|	SALE|	55|
|B0003|	dhfkzmf09|	에어팟 맥스|	에어팟 맥스 스카이 블루 색상 판매합니다.|	450000|	2022-11-26|	DONE|	67|
|B0004|	sangjune1|	파파야나인 포르쉐 푸쉬카|	예민하신분은 피해주세요	|30000|	2022-11-30|	DONE|	78|

*USED_GOODS_BOARD*
|USER_ID|	NICKNAME|	CITY|	STREET_ADDRESS1|	STREET_ADDRESS2|	TLNO|
|---|---|---|---|---|---|
|cjfwls91|	점심만금식|	성남시|	분당구 내정로 185|	501호|	01036344964|
|zkzkdh1|	후후후|	성남시|	분당구 내정로 35|	가동 1202호|	01032777543|
|spdlqj12|	크크큭|	성남시|	분당구 수내로 206|	2019동 801호|	01087234922|
|xlqpfh2|	잉여킹|	성남시|	분당구 수내로 1|	001-004|	01064534911|
|dhfkzmf09|	찐찐|	성남시|	분당구 수내로 13|	A동 1107호|	01053422914|

<br>

**Sample Output**

|USER_ID|	NICKNAME|	TOTAL_SALES|
|---|---|---|
|zkzkdh1|	후후후|	700000|

<br>

### Solving

```sql
WITH USER_STAT AS (
    SELECT WRITER_ID
         , SUM(PRICE) AS TOTAL_SALES
    FROM USED_GOODS_BOARD
    WHERE STATUS = 'DONE'
    GROUP BY WRITER_ID
    HAVING SUM(PRICE) >= 700000
)    

SELECT U.USER_ID
     , U.NICKNAME
     , S.TOTAL_SALES
FROM USER_STAT S
 LEFT JOIN USED_GOODS_USER U ON S.WRITER_ID = U.USER_ID
ORDER BY TOTAL_SALES
```
