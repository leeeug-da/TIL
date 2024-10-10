### Topic
- SELECT
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SELECT) (조건에 맞는 도서 리스트 출력하기)
- *table* : BOOK

<br>

**BOOK**
|column|type|nullable|
|---|---|---|
|BOOK_ID|	INTEGER|	FALSE|
|CATEGORY|	VARCHAR(N)|	FALSE|	
|AUTHOR_ID|	INTEGER|	FALSE|	
|PRICE|	INTEGER|	FALSE|	
|PUBLISHED_DATE|	DATE|	FALSE|	

<br>

### Problem
`BOOK` 테이블에서 `2021`년에 출판된 '`인문`' 카테고리에 속하는 도서 리스트를 찾아서 도서 ID(`BOOK_ID`), 출판일 (`PUBLISHED_DATE`)을 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*BOOK*
|BOOK_ID|	CATEGORY|	AUTHOR_ID|	PRICE|	PUBLISHED_DATE|
|---|---|---|---|---|
|1|	인문|	1|	10000|	2020-01-01|
|2|	경제|	2|	9000|	2021-02-05|
|3|	인문|	2|	11000|	2021-04-11|
|4|	인문|	3|	10000|	2021-03-15|
|5|	생활|	1|	12000|	2021-01-10|

<br>

**Sample Output**

|BOOK_ID|	PUBLISHED_DATE|
|---|---|
|4|	2021-03-15|
|3|	2021-04-11|
<br>

### Solving

```sql
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK
WHERE YEAR(PUBLISHED_DATE) = 2021
  AND CATEGORY = '인문'
ORDER BY PUBLISHED_DATE                      
```
