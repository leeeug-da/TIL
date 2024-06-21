### Topic
- Subquery
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (그룹별 조건에 맞는 식당 목록 출력하기)
- *table* : MEMBER_PROFILE, REST_REVIEW

**MEMBER_PROFILE**
|column|type|
|---|---|
|MEMBER_ID|VARCHAR|
|MEMBER_NAME|VARCHAR|
|TLNO|VARCHAR|
|GENDER|VARCHAR|
|DATE_OF_BIRTH|DATE|

`MEMBER_PROFILE` 테이블은 다음과 같으며 `MEMBER_ID`, `MEMBER_NAME`, `TLNO`, `GENDER`, `DATE_OF_BIRTH`는 회원 ID, 회원 이름, 회원 연락처, 성별, 생년월일을 의미합니다.

**REST_REVIEW**
|column|type|
|---|---|
|REVIEW_ID|VARCHAR|
|REST_ID|VARCHAR|
|MEMBER_ID|VARCHAR|
|REVIEW_SCORE|NUMBER|
|REVIEW_TEXT|VARCHAR|
|REVIEW_DATE|DATE|

`REST_REVIEW` 테이블은 다음과 같으며 `REVIEW_ID`, `REST_ID`, `MEMBER_ID`, `REVIEW_SCORE`, `REVIEW_TEXT`, `REVIEW_DATE`는 각각 리뷰 ID, 식당 ID, 회원 ID, 점수, 리뷰 텍스트, 리뷰 작성일을 의미합니다.

### Problem 
`MEMBER_PROFILE`와 `REST_REVIEW` 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요. 회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.
`REVIEW_DATE`의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.



**Sample Input**

*MEMBER_PROFILE*
|MEMBER_ID	|MEMBER_NAME|	TLNO|	GENDER|	DATE_OF_BIRTH|
|---|---|---|---|---|
|jiho92@naver.com|	이지호|	01076432111|	W|	1992-02-12|
|jiyoon22@hotmail.com|	김지윤|	01032324117|	W|	1992-02-22|
|jihoon93@hanmail.net|	김지훈|	01023258688|	M|	1993-02-23|
|seoyeons@naver.com|	박서연|	01076482209|	W|	1993-03-16|
|yelin1130@gmail.com|	조예린|	01017626711|	W|	1990-11-30|

*REST_REVIEW*
|REVIEW_ID|	REST_ID|	MEMBER_ID|	REVIEW_SCORE|	REVIEW_TEXT|	REVIEW_DATE|
|---|---|---|---|---|---|
|R000000065|	00028|	soobin97@naver.com|	5|	부찌 국물에서 샤브샤브 맛이나고 깔끔|	2022-04-12|
|R000000066|	00039|	yelin1130@gmail.com|	5|	김치찌개 최곱니다.|	2022-02-12|
|R000000067|	00028|	yelin1130@gmail.com|	5|	햄이 많아서 좋아요|	2022-02-22|
|R000000068|	00035|	ksyi0316@gmail.com|	5|	숙성회가 끝내줍니다.|	2022-02-15|
|R000000069|	00035|	yoonsy95@naver.com|	4|	비린내가 전혀없어요.|	2022-04-16|

<br>

**Sample Output**
|MEMBER_NAME|	REVIEW_TEXT|	REVIEW_DATE|
|---|---|---|
|조예린|	김치찌개 최곱니다.|	2022-02-12|
|조예린|	햄이 많아서 좋아요|	2022-02-22|


<br>

### Solving
```sql
-- 리뷰를 가장 많이 작성한 회원 
-- 회원 이름(MEMBER_NAME), 리뷰 텍스트(REVIEW_TEXT), 리뷰 작성일(REVIEW_DATE)
-- 리뷰 작성일 오름차순, 리뷰 텍스트 오름차순 

SELECT M.MEMBER_NAME
     , R.REVIEW_TEXT
     , DATE_FORMAT(R.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
FROM MEMBER_PROFILE M 
 JOIN REST_REVIEW R ON M.MEMBER_ID = R.MEMBER_ID
WHERE M.MEMBER_ID = (SELECT MEMBER_ID
                     FROM REST_REVIEW
                     GROUP BY MEMBER_ID
                     ORDER BY COUNT(REVIEW_ID) DESC
                     LIMIT 1)
ORDER BY R.REVIEW_DATE, R.REVIEW_TEXT
```
