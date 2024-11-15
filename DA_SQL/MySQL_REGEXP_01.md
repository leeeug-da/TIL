### Topic
- REGEXP (정규표현식)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (1517. Find Users With Valid E-Mails)
- *table* : Users

**Users**
|column|type|
|---|---|
| user_id       | int     |
| name          | varchar |
| mail          | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains information of the users signed up in a website. Some e-mails are invalid.


<br>

### Problem 
Write a solution to find the users who have valid emails.

A valid e-mail has a prefix name and a domain where:

The prefix name is a string that may contain letters (upper or lower case), digits, underscore `'_'`, period `'.'`, and/or dash `'-'`. The prefix name must start with a letter.
The domain is `'@leetcode.com'`.
Return the result table in any order.

The result format is in the following example.

<br>

**Sample Input**
| user_id | name      | mail                    |
|---|---|---|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

<br>

**Sample Output**
| user_id | name      | mail                    |
|---|---|---|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |


<br>

### Solving
```sql
SELECT user_id, name, mail
FROM Users
WHERE regexp_like (mail,'^[a-z]+[0-9a-zA-Z_.-]*@leetcode[.]{1}com$')

-- ^[a-z] 알파벳이 한 개 이상인 문자열로 시작
-- [0-9a-zA-Z_.-]*   영문자, 숫자, 밑줄(_), 점(.), 하이픈(-)이 0번 이상 
-- @leetcode[.]{1}com$   @leetcode.com 으로 마무리
```
