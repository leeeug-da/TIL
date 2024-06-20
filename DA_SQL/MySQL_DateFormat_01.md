### Topic
- Date Format
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (조건에 맞는 도서와 저자 리스트 출력하기)
- *table* : BOOK, AUTHOR

<br>

**BOOK**
|column|type|
|---|---|
|BOOK_ID|INTEGER|
|CATEGORY|VARCHAR|
|AUTHOR_ID|INTEGER|
|PRICE|INTEGER|
|PUBLISHED_DATE|DATE|


**AUTHOR**
|column|type|
|---|---|
|AUTHOR_ID|INTEGER|
|AUTHOR_NAME|VARCHAR|


<br>

### Problem 
'경제' 카테고리에 속하는 도서들의 도서 ID(BOOK_ID), 저자명(AUTHOR_NAME), 출판일(PUBLISHED_DATE) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 출판일을 기준으로 오름차순 정렬해주세요. PUBLISHED_DATE의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.
<br>

**Sample Input**

*BOOK*
|BOOK_ID|CATEGORY|AUTHOR_ID|PRICE|PUBLISHED_DATE|
|---|---|---|---|---|
|1|인문|1|10000|2020-01-01|
|2|경제|1|9000|2021-04-11|
|3|경제|2|11000|2021-02-05|

*AUTHOR*
|AUTHOR_ID|AUTHOR_NAME|
|---|---|
|1|홍길동|
|2|김영호|

<br>

**Sample Output**

|BOOK_ID|AUTHOR_NAME|PUBLISHED_DATE|
|---|---|---|
|3|김영호|2021-02-05|
|2|홍길동|2021-04-11|

<br>

### Solving

```sql
SELECT B.BOOK_ID
     , A.AUTHOR_NAME
     , DATE_FORMAT(B.PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK B 
 JOIN AUTHOR A ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE B.CATEGORY = '경제'
ORDER BY B.PUBLISHED_DATE
```