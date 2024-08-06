### Topic
- GROUP BY
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (GROUP BY) (진료과별 총 예약 횟수 출력하기)
- *table* : APPOINTMENT

<br>

**APPOINTMENT**
|column|type|nullable|
|---|---|---|
|APNT_YMD|	TIMESTAMP|	FALSE|
|APNT_NO|	NUMBER(5)|	FALSE|
|PT_NO|	VARCHAR(10)|	FALSE|
|MCDP_CD|	VARCHAR(6)|	FALSE|
|MDDR_ID|	VARCHAR(10)|	FALSE|
|APNT_CNCL_YN|	VARCHAR(1)|	TRUE|
|APNT_CNCL_YMD|	DATE|	TRUE|

`APPOINTMENT` 테이블은 다음과 같으며 `APNT_YMD`, `APNT_NO`, `PT_NO`, `MCDP_CD`, `MDDR_ID`, `APNT_CNCL_YN`, `APNT_CNCL_YMD`는 각각 진료예약일시, 진료예약번호, 환자번호, 진료과코드, 의사ID, 예약취소여부, 예약취소날짜를 나타냅니다.

<br>

**Sample Input**

*APPOINTMENT*
|APNT_YMD|	APNT_NO|	PT_NO|	MCDP_CD|	MDDR_ID|	APNT_CNCL_YN|	APNT_CNCL_YMD|
|---|---|---|---|---|---|---|
|2022-04-14| 09:30:00.000000|	47|	PT22000064	|GS|	DR20170123|	N|	NULL|
|2022-04-15| 10:30:00.000000|	48|	PT22000065|	OB|	DR20100231|	N|	NULL|
|2022-05-15| 17:30:00.000000|	49|	PT22000086|	OB|	DR20100231|	N|	NULL|
|2022-05-18| 10:30:00.000000|	52|	PT22000019|	GS|	DR20100039|	N|	NULL|
|2022-05-19| 12:00:00.000000|	53|	PT22000020|	FM|	DR20010112|	N|	NULL|

<br>

**Sample Output**

|진료과코드|	5월예약건수|
|---|---|
|OB|	1|
|OS|	1|
|CS|	2|
|FM|	2|
|GS|	2|

<br>

### Solving

```sql
SELECT MCDP_CD AS '진료과코드'
     , COUNT(DISTINCT APNT_NO) AS '5월예약건수'
FROM APPOINTMENT
WHERE DATE_FORMAT(APNT_YMD, '%Y-%m-%d') BETWEEN '2022-05-01' AND '2022-05-31'
GROUP BY MCDP_CD
ORDER BY COUNT(DISTINCT APNT_NO), MCDP_CD
```
