### Topic
- Join (Natural Join)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Programmers (SQL 고득점 Kit) (SUM, MAX< MIN) (물고기 종류 별 대어 찾기)
- *table* : FISH_INFO, FISH_NAME_INFO

<br>

**FISH_INFO**
|column|type|
|---|---|
|ID|INTEGER|
|FISH_TYPE|INTEGER|
|LENGTH|FLOAT|
|TIME|DATE|

`FISH_INFO` 테이블의 구조는 다음과 같으며 `ID`, `FISH_TYPE`, `LENGTH`, `TIME`은 각각 잡은 물고기의 ID, 물고기의 종류(숫자), 잡은 물고기의 길이(cm), 물고기를 잡은 날짜를 나타냅니다. 단, 잡은 물고기의 길이가 10cm 이하일 경우에는 `LENGTH` 가 NULL 이며, `LENGTH` 에 NULL 만 있는 경우는 없습니다.

<br>

**FISH_NAME_INFO**
|column|type|
|---|---|
|FISH_TYPE|INTEGER|
|FISH_NAME|VARCHAR|

`FISH_NAME_INFO` 테이블은 물고기의 이름에 대한 정보를 담고 있습니다. `FISH_NAME_INFO` 테이블의 구조는 다음과 같으며, `FISH_TYPE`, `FISH_NAME` 은 각각 물고기의 종류(숫자), 물고기의 이름(문자) 입니다.

<br>

### Problem 
물고기 종류 별로 가장 큰 물고기의 ID, 물고기 이름, 길이를 출력하는 SQL 문을 작성해주세요.

물고기의 ID 컬럼명은 `ID`, 이름 컬럼명은 `FISH_NAME`, 길이 컬럼명은 `LENGTH`로 해주세요.
결과는 물고기의 ID에 대해 오름차순 정렬해주세요.
단, 물고기 종류별 가장 큰 물고기는 1마리만 있으며 10cm 이하의 물고기가 가장 큰 경우는 없습니다.

<br>

**Sample Input**

*FISH_INFO*

|ID|	FISH_TYPE|	LENGTH|	TIME|
|---|---|---|---|
|0|	0|	30|	2021/12/04|
|1|	0|	50|	2020/03/07|
|2|	0|	40|	2020/03/07|
|3|	1|	20|	2022/03/09|
|4|	1|	NULL|	2022/04/08|
|5|	2|	13|	2021/04/28|
|6|	0|	60|	2021/07/27|
|7|	0|	55|	2021/01/18|
|8|	2|	73|	2020/01/28|
|9|	1|	73|	2021/04/08|
|10|	2|	22|	2020/06/28|
|11|	2|	17|	2022/12/23|


*FISH_NAME_INFO*

|FISH_TYPE|	FISH_NAME|
|---|---|
|0|	BASS|
|1|	SNAPPER|
|2|	ANCHOVY|

<br>

**Sample Output**

|ID|	FISH_NAME|	LENGTH|
|---|---|---|
|6|	BASS|	60|
|8|	ANCHOVY|	73|
|9|	SNAPPER|	73|

<br>

### Solving

```sql
-- 물고기 종류 별로 가장 큰 물고기의 
-- ID, FISH_NAME, LENGTH
-- ID ASC

WITH MAX_FISH AS (
    SELECT FISH_TYPE
         , MAX(LENGTH) AS LENGTH
         , FISH_NAME
    FROM FISH_INFO
     NATURAL JOIN FISH_NAME_INFO
    GROUP BY FISH_TYPE, FISH_NAME
)

SELECT ID
     , FISH_NAME
     , LENGTH
FROM FISH_INFO FI
 NATURAL JOIN MAX_FISH M 
ORDER BY ID
```

<br>

### Study Note

#### 📍Natural Join
- 등가 조인하는 방법 중 하나
- 동일한 타입과 이름을 가진 컬럼을 조인함
- 두 테이블의 동일한 이름을 가지는 칼럼이 모두 조인됨
- 동일한 칼럼을 내부적으로 찾게 되므로 테이블 별칭(Alias)를 주면 오류가 발생함 
- 반드시 두 테이블 간의 동일한 이름, 타입을 가진 컬럼이 필요
- 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인해 사용됨
- 동일한 이름을 갖는 컬럼이 있지만 데이터 타입이 다르면 에러가 발생함
- 조인하는 테이블 간의 동일 컬럼이 SELECT절에 기술되도 테이블 이름을 생략해야 함 
