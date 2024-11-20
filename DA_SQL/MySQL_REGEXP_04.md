### Topic
- REGEXP (정규표현식)
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : Leetcode (SQL 50) (1527. Patients With a Condition)
- *table* : Patients

**Users**
|column|type|
|---|---|
| patient_id   | int     |
| patient_name | varchar |
| conditions   | varchar |

patient_id is the primary key (column with unique values) for this table.
'conditions' contains 0 or more code separated by spaces. 
This table contains information of the patients in the hospital.



<br>

### Problem 
Write a solution to find the patient_id, patient_name, and conditions of the patients who have Type I Diabetes. Type I Diabetes always starts with `DIAB1` prefix.

Return the result table in any order.

The result format is in the following example.



<br>

**Sample Input**
| patient_id | patient_name | conditions   |
|---|---|---|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

<br>

**Sample Output**
| patient_id | patient_name | conditions   |
|---|---|---|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 | 


<br>

### Solving
```sql
SELECT patient_id, patient_name, conditions
FROM Patients
WHERE conditions REGEXP '^DIAB1| DIAB1'
```
