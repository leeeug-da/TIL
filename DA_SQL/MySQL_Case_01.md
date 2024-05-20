### Topic
- Case
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank 
- *table* : TRIANGLES

|column|type|description|  
|---|---|---|
|integer|A|length of triangle's side|
|integer|B|length of triangle's side|
|integer|C|length of triangle's side|




### Problem 
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with  sides of equal length.
- Isosceles: It's a triangle with  sides of equal length.
- Scalene: It's a triangle with  sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

**Sample Input**
|A|B|C|
|---|---|---|
|20|20|23|
|20|20|20|
|20|21|22|
|13|14|30|

**Sample Output**

Isosceles <br>
Equilateral <br>
Scalene <br>
Not A Triangle


**Explanation**

Values in the tuple (20,20,23) form an Isosceles triangle, because A=B.
Values in the tuple (20,20,20) form an Equilateral triangle, because A=B=C. 
Values in the tuple (20,21,22) form a Scalene triangle, because A!=B!=C.
Values in the tuple (13,14,30) cannot form a triangle because the combined value of sides A and B is not larger than that of side C.


### Solving

```sql
SELECT CASE 
            WHEN A = B AND B = C THEN 'Equilateral'
            WHEN A + B <= C THEN 'Not A Triangle'
            WHEN A != B AND B != C AND A != C THEN 'Scalene'
            ELSE 'Isosceles'
        END 
FROM TRIANGLES;
```

