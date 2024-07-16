### Topic
- Funnel Analysis
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : solvesql 
- *table* : ga (데이터리안 블로그 GA 로그 (2022년 1월))

**ga**
|type|column|
|---|---|
|datetime| event_timestamp_kst|
|string| user_pseudo_id|
|string| ga_session_id|
|string| event_name|
|string| page_location|
|string| page_title|
|string| source|
|string| medium|
|string| continent|
|string| country|
|string| device_category|


<br>

### Problem 
`ga` 테이블에는 데이터리안 웹사이트에 접속한 사용자의 행동 데이터가 들어있습니다. 사용자가 사이트에 접속하면 세션이 생성되고, 각 세션에 ID가 부여됩니다. 사용자가 웹 브라우저를 종료하거나, 일정 시간이 흐르는 등 여러가지 이유로 세션이 새로 만들어질 수 있습니다. 구체적인 세션에 대한 내용은 GA 문서를 참고해주세요.

전체 세션을 아래 그림처럼 입문반 페이지를 본 세션과 안 본 세션으로 나누어 집계하려고 합니다. 아래에 기재된 데이터 설명을 바탕으로 쿼리를 작성해주세요.

- `user_pseudo_id` 컬럼은 이벤트를 발생시킨 사용자의 고유 ID 입니다.
- `event_name` 컬럼은 사용자가 발생시킨 이벤트를 의미합니다.
- `page_title` 컬럼은 사용자가 이벤트를 발생시킨 페이지의 제목입니다.
- `ga_session_id` 컬럼은 세션마다 부여된 세션 ID 입니다. 세션 ID는 같은 사용자에 대해서는 고유(unique)하지만, 사용자가 다르면 겹칠 수 있습니다.
  
`user_pseudo_id` 와 `ga_session_id` 컬럼은 N:M 관계입니다. 즉, 한 명의 사용자가 여러 개의 `ga_session_id` 값을 가질 수 있습니다. 개별 세션을 특정하려면 `user_pseudo_id` 와 `ga_session_id` 컬럼을 모두 고려해야 합니다.
예를 들어, 아래 데이터에서 ‘백문이불여일타 SQL 캠프 입문반' 을 본 사용자의 수는 2명(xSXcHvtWoA, KE8fB0xo3Z)이고, 개별 세션의 수는 4개입니다. `ga_session_id` 컬럼의 값이 ‘1642676241’인 사용자가 2명이지만, `user_pseudo_id`가 다르므로 각각 다른 세션으로 계산합니다.

입문반 페이지를 본 세션은 아래 조건으로 찾을 수 있습니다.

- `page_title` = “백문이불여일타 SQL 캠프 입문반”
- `event_name` = “page_view”
  
`ga` 테이블에 있는 전체 기간 동안, 입문반 페이지를 본 세션과 그렇지 않은 세션의 수를 집계하는 쿼리를 작성해주세요. 쿼리 결과에는 아래 컬럼이 포함되어야 합니다.

- `total` - 전체 세션 수
- `pv_no` - 입문반 페이지를 안 본 세션 수 (= `total` - `pv_yes`)
- `pv_yes` - 입문반 페이지를 본 세션 수


### Solving
```sql
WITH pv AS (
  SELECT user_pseudo_id
      , ga_session_id
      , event_name
      , page_title
  FROM ga
  WHERE page_title = '백문이불여일타 SQL 캠프 입문반'
    AND event_name = 'page_view'
)

SELECT COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id) AS total
     , COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id) - COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv_no
     , COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv_yes
FROM ga
 LEFT JOIN pv ON ga.user_pseudo_id = pv.user_pseudo_id
             AND ga.ga_session_id = pv.ga_session_id
```
