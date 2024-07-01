### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (상품을 구매한 회원 비율 구하기)
- *table* : USER_INFO, ONLINE_SALE

**USER_INFO**
|column|type|
|---|---|
|USER_ID|INTEGER|
|GENDER|TINYINT(1)|
|AGE|INTEGER|
|JOINED|DATE|

`USER_INFO` 테이블은 아래와 같은 구조로 되어있으며 `USER_ID`, `GENDER`, `AGE`, `JOINED`는 각각 회원 ID, 성별, 나이, 가입일을 나타냅니다.

**ONLINE_SALE**
|column|type|
|---|---|
|ONLINE_SALE_ID|INTEGER|
|USER_ID|INTEGER|
|PRODUCT_ID|INTEGER|
|SALES_AMOUNT|INTEGER|
|SALES_DATE|DATE|

`ONLINE_SALE` 테이블은 아래와 같은 구조로 되어있으며 `ONLINE_SALE_ID`, `USER_ID`, `PRODUCT_ID`, `SALES_AMOUNT`, `SALES_DATE`는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다. 동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.

### Problem 
`USER_INFO` 테이블과 `ONLINE_SALE` 테이블에서 2021년에 가입한 전체 회원들 중 상품을 구매한 회원수와 상품을 구매한 회원의 비율(=2021년에 가입한 회원 중 상품을 구매한 회원수 / 2021년에 가입한 전체 회원 수)을 년, 월 별로 출력하는 SQL문을 작성해주세요. 상품을 구매한 회원의 비율은 소수점 두번째자리에서 반올림하고, 전체 결과는 년을 기준으로 오름차순 정렬해주시고 년이 같다면 월을 기준으로 오름차순 정렬해주세요.



**Sample Input**

*USER_INFO*
|USER_ID|GENDER|AGE|JOINED|
|---|---|---|---|
|1|	1|	26|	2021-06-01|
|2|	NULL|	NULL|	2021-06-25|
|3|	0|	NULL|	2021-06-30|
|4|	0|	31|	2021-07-03|
|5|	1|	25|	2022-01-09|
|6|	1|	33|	2022-02-14|

*ONLINE_SALE*
|ONLINE_SALE_ID|	USER_ID|	PRODUCT_ID|	SALES_AMOUNT|	SALES_DATE|
|---|---|---|---|---|
|1|	1|	54|	1|	2022-01-01|
|2|	1|	3|	2|	2022-01-25|
|3|	4|	34|	1|	2022-01-30|
|4|	6|	253|	3|	2022-02-03|
|5|	2|	31|	2|	2022-02-09|
|6|	5|	35|	1|	2022-02-14|
|7|	5|	57|	1|	2022-02-18|

<br>

**Sample Output**
|YEAR|	MONTH|	PURCHASED_USERS|	PUCHASED_RATIO|
|---|---|---|---|
|2022|	1|	2|	0.5|
|2022|	2|	1|	0.3|


<br>

### Solving
```sql
-- 2021년에 가입한 
-- PURCHASED_USERS 상품을 구매한 회원수
-- PURCHASED_RATIO 상품을 구매한 회원수 / 전체 회원 수 -> ROUND(,2)
-- YEAR 년, MONTH 월 별로 출력 
-- YEAR ASC, MONTH ASC


SELECT DATE_FORMAT(S.SALES_DATE, '%Y') AS YEAR
     , DATE_FORMAT(S.SALES_DATE, '%m') AS MONTH
     , COUNT(DISTINCT S.USER_ID) AS PURCHASED_USERS # 구매한 회원
     , ROUND(COUNT(DISTINCT S.USER_ID) /  # 구매한 회원
            (SELECT COUNT(DISTINCT USER_ID) FROM USER_INFO WHERE JOINED LIKE '2021%')    # 전체 회원 
            , 1) AS PURCHASED_RATIO
FROM USER_INFO U
 RIGHT JOIN ONLINE_SALE S USING (USER_ID)
WHERE U.JOINED LIKE '2021%'
GROUP BY YEAR, MONTH
ORDER BY YEAR, MONTH




```
