### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (카테고리 별 도서 판매량 집계하기)
- *table* : BOOK, BOOK_SALES

<br>

**BOOK**
|column|type|
|---|---|
|BOOK_ID|INTEGER|
|CATEGORY|VARCHAR|
|AUTHOR_ID|INTEGER|
|PRICE|INTEGER|
|PUBLISHED_DATE|DATE|

`BOOK` 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

**BOOK_SALES**
|column|type|
|---|---|
|BOOK_ID|INTEGER|
|SALES_DATE|DATE|
|SALES|INTEGER|

`BOOK_SALES` 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

<br>

### Problem 
`2022년 1월`의 카테고리 별 도서 판매량을 합산하고, 카테고리(`CATEGORY`), 총 판매량(`TOTAL_SALES`) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 카테고리명을 기준으로 오름차순 정렬해주세요.

<br>

**Sample Input**

*BOOK*

|BOOK_ID|	CATEGORY|	AUTHOR_ID|	PRICE|	PUBLISHED_DATE|
|---|---|---|---|---|
|1|	인문|	1|	10000|	2020-01-01|
|2|	경제|	1|	9000|	2021-02-05|
|3|	경제|	2|	9000|	2021-03-11|

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

|CATEGORY|	TOTAL_SALES|
|---|---|
|경제|	16|
|인문|	3|

<br>

### Solving

```sql
SELECT B.CATEGORY
     , SUM(BS.SALES) AS TOTAL_SALES
FROM BOOK B
 INNER JOIN BOOK_SALES BS ON B.BOOK_ID = BS.BOOK_ID
WHERE BS.SALES_DATE BETWEEN '2022-01-01' AND '2022-01-31'
GROUP BY B.CATEGORY
ORDER BY CATEGORY
```
