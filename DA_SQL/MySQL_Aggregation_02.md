### Topic
- Aggregation
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (Average Population)
- *table* : CITY

**CITY**
|column|type|
|---|---|
|ID|NUMBER|
|NAME|VARCHAR2(17)|
|COUNTRYCODE|VARCHAR2(3)|
|DISTRICT|VARCHAR2(20)|
|POPULATION|NUMBER|




### Problem 
Query the average population for all cities in CITY, rounded down to the nearest integer.



### Solving

```sql
SELECT FLOOR(AVG(POPULATION))
FROM CITY;
```

