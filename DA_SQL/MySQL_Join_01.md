### Topic
- Join
  
### Language
- MySQL

### Data
- *database* : 
- *platform* : HackerRank (African Cities)
- *table* : CITY, COUNTRY

**CITY**
|column|type|
|---|---|
|ID|NUMBER|
|NAME|VARCHAR2(17)|
|COUNTRYCODE|VARCHAR2(3)|
|DISTRICT|VARCHAR2(20)|
|POPULATION|NUMBER|

**COUNTRY**
|column|type|
|---|---|
|CODE|VARCHAR2(3)|
|NAME|VARCHAR2(44)|
|CONTINENT|VARCHAR2(13)|
|REGION|VARCHAR2(25)|
|SURFACEAREA|NUMBER|
|INDEPYEAR|VARCHAR2(5)|
|POPULATION|NUMBER|
|LIFEEXPECTANCY|VARCHAR2(4)|
|GNP|NUMBER|
|GNPOLD|VARCHAR2(9)|
|LOCALNAME|VARCHAR2(44)|
|GOVERNMENTFORM|VARCHAR2(44)|
|HEADOFSTATE|VARCHAR2(32)|
|CAPITAL|VARCHAR2(4)|
|CODE2|VARCHAR2(2)|




### Problem 
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.


### Solving

```sql
SELECT cty.NAME
FROM CITY cty
    JOIN COUNTRY cnt ON cty.COUNTRYCODE = cnt.CODE
WHERE cnt.CONTINENT = 'Africa';
```

