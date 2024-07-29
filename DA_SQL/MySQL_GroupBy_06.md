### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (저자 별 카테고리 별 매출액 집계하기)
- *table* : BOOK, AUTHOR, BOOK_SALES

<br>

**BOOK**
|column|type|nullable|description|
|---|---|---|---|
|BOOK_ID|	INTEGER|	FALSE|	도서 ID|
|CATEGORY|	VARCHAR(N)|	FALSE|	카테고리 (경제, 인문, 소설, 생활, 기술)|
|AUTHOR_ID|	INTEGER|	FALSE|	저자 ID|
|PRICE|	INTEGER|	FALSE|	판매가 (원)|
|PUBLISHED_DATE|	DATE|	FALSE|	출판일|

<br>

**AUTHOR**
|column|type|nullable|description|
|---|---|---|---|
|AUTHOR_ID|	INTEGER|	FALSE|	저자 ID|
|AUTHOR_NAME|	VARCHAR(N)|	FALSE|	저자명|

<br>

**BOOK_SALES**
|column|type|nullable|description|
|---|---|---|---|
|BOOK_ID|	INTEGER|	FALSE|	도서 ID|
|SALES_DATE|	DATE|	FALSE|	판매일|
|SALES|	INTEGER|	FALSE|	판매량|

<br>

### Problem 
`2022년 1월`의 도서 판매 데이터를 기준으로 저자 별, 카테고리 별 매출액(`TOTAL_SALES = 판매량 * 판매가`) 을 구하여, 저자 ID(`AUTHOR_ID`), 저자명(`AUTHOR_NAME`), 카테고리(`CATEGORY`), 매출액(`SALES`) 리스트를 출력하는 SQL문을 작성해주세요.

<br>

**Sample Input**

*BOOK*
|BOOK_ID|	CATEGORY|	AUTHOR_ID|	PRICE|	PUBLISHED_DATE|
|---|---|---|---|---|
|1|	인문|	1|	10000|	2020-01-01|
|2|	경제|	1|	9000|	2021-02-05|
|3|	경제|	2|	9000|	2021-03-11|

<br>

*AUTHOR*
|AUTHOR_ID|	AUTHOR_NAME|
|---|---|
|1|	홍길동|
|2|	김영호|

<br>

*BOOK_SALES*
|BOOK_ID|	SALES_DATE|	SALES|
|---|---|---|
|1|	2022-01-01|	2|
|2|	2022-01-02|	3|
|1|	2022-01-05|	1|
|2|	2022-01-20|	5|
|2|	2022-01-21|	6|
|3|	2022-01-22|	2|
|2|	2022-02-11|	3|

<br>

**Sample Output**

|AUTHOR_ID|	AUTHOR_NAME|	CATEGORY|	TOTAL_SALES|
|---|---|---|---|
|1|	홍길동|	인문|	30000|
|1|	홍길동|	경제|	126000|
|2|	김영호|	경제|	18000|

<br>

### Solving

```sql
WITH AUTHOR_SALES AS (
    SELECT B.AUTHOR_ID
         , B.CATEGORY
         , SUM(B.PRICE * BS.SALES) AS TOTAL_SALES
    FROM BOOK B
     JOIN BOOK_SALES BS ON B.BOOK_ID = BS.BOOK_ID
    WHERE BS.SALES_DATE BETWEEN '2022-01-01' AND '2022-01-31'
    GROUP BY B.AUTHOR_ID, B.CATEGORY
)

SELECT ATS.AUTHOR_ID
     , A.AUTHOR_NAME
     , ATS.CATEGORY
     , ATS.TOTAL_SALES
FROM AUTHOR_SALES AS ATS
 JOIN AUTHOR A ON ATS.AUTHOR_ID = A.AUTHOR_ID
ORDER BY AUTHOR_ID, CATEGORY DESC
```
