### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (년, 월, 성별 별 상품 구매 회원 수 구하기)
- *table* : USER_INFO, ONLINE_SALE

<br>

**USER_INFO**
|column|type|nullable|
|---|---|---|
|USER_ID|	INTEGER|	FALSE|
|GENDER|	TINYINT(1)|	TRUE|
|AGE|	INTEGER|	TRUE|
|JOINED|	DATE|	FALSE|

`USER_INFO` 테이블은 아래와 같은 구조로 되어있으며 `USER_ID`, `GENDER`, `AGE`, `JOINED`는 각각 회원 ID, 성별, 나이, 가입일을 나타냅니다.

`GENDER` 컬럼은 비어있거나 0 또는 1의 값을 가지며 0인 경우 남자를, 1인 경우는 여자를 나타냅니다.

<br>

**ONLINE_SALE**
|column|type|nullable|
|---|---|---|
|ONLINE_SALE_ID|	INTEGER|	FALSE|
|USER_ID|	INTEGER|	FALSE|
|PRODUCT_ID|	INTEGER|	FALSE|
|SALES_AMOUNT|	INTEGER|	FALSE|
|SALES_DATE|	DATE|	FALSE|

`ONLINE_SALE` 테이블은 아래와 같은 구조로 되어있으며, `ONLINE_SALE_ID`, `USER_ID`, `PRODUCT_ID`, `SALES_AMOUNT`, `SALES_DATE`는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.

동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.

<br>

### Problem
`USER_INFO` 테이블과 `ONLINE_SALE` 테이블에서 년, 월, 성별 별로 상품을 구매한 회원수를 집계하는 SQL문을 작성해주세요. 결과는 년, 월, 성별을 기준으로 오름차순 정렬해주세요. 이때, 성별 정보가 없는 경우 결과에서 제외해주세요.

<br>

**Sample Input**

*USER_INFO*
|USER_ID|	GENDER|	AGE|	JOINED|
|---|---|---|---|
|1|	1|	26|	2021-06-01|
|2|	NULL|	NULL|	2021-06-25|
|3|	0|	NULL|	2021-06-30|
|4|	0|	31|	2021-07-03|
|5|	1|	25|	2021-07-09|
|6|	1|	33|	2021-07-14|

*ONLINE_SALE*
|ONLINE_SALE_ID|	USER_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|---|
|1|	1|	54|	1|	2022-01-01|
|2|	1|	3|	2|	2022-01-25|
|3|	4|	34|	1|	2022-01-30|
|4|	6|	253|	3|	2022-02-03|
|5|	2|	31|	2|	2022-02-09|

<br>

**Sample Output**

|YEAR|	MONTH|	GENDER|	USERS|
|---|---|---|---|
|2022|	1|	0|	1|
|2022|	1|	1|	1|
|2022|	2|	1|	2|

<br>

### Solving

```sql
SELECT YEAR(S.SALES_DATE) AS YEAR
     , MONTH(S.SALES_DATE) AS MONTH
     , U.GENDER
     , COUNT(DISTINCT S.USER_ID) AS USERS
FROM USER_INFO U
 INNER JOIN ONLINE_SALE S ON U.USER_ID = S.USER_ID
WHERE U.GENDER IS NOT NUll
GROUP BY YEAR(S.SALES_DATE), MONTH(S.SALES_DATE), U.GENDER
ORDER BY YEAR, MONTH, GENDER
```
