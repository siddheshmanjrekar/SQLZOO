# SELECT from WORLD Tutorial

1. Introduction
```sql
SELECT name, continent, population FROM world
```

2. Large Countries
Show the name for the countries that have a population of at least 200 million
```sql
SELECT name FROM world
WHERE population >= 200000000
```

3. Per capita GDP
Give the name and the per capita GDP for those countries with a population of at least 200 million.
```sql
SELECT name, (gdp/population) from world
WHERE population >= 200000000 
```

4. South America In millions
Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.
```sql
SELECT name,population/1000000 from world
WHERE continent = 'South America'
```

5. France, Germany, Italy
Show the name and population for France, Germany, Italy
```sql
SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

6. United
Show the countries which have a name that includes the word 'United'
```sql
SELECT name FROM world
WHERE name LIKE '%United%'
```

7. Two ways to be big
Show the countries that are big by area or big by population. Show name, population and area.
```sql
SELECT name, population, area FROM world
WHERE area> 3000000 or population>250000000
```

8. One or the other (but not both)
Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.
```sql
SELECT name, population, area FROM world
WHERE area> 3000000 xor population>250000000
```

9. Rounding
For South America show population in millions and GDP in billions both to 2 decimal places.
```sql
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2) FROM world
WHERE continent = 'South America'
 ```
 
 10. Trillion dollar economies
 Show per-capita GDP for the trillion dollar countries to the nearest $1000.
```sql
SELECT name, ROUND(gdp/population,-3) FROM world
WHERE gdp>= 1000000000000
```

11. Name and capital have the same length
Show the name and capital where the name and the capital have the same number of characters.
```sql
SELECT name, capital
  FROM world
 WHERE LENGTH(name) = LENGTH(capital)
```

12. Matching name and capital
Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.
```sql
SELECT name, capital
FROM world
WHERE (LEFT(name,1) = LEFT(capital,1)) and name <> capital
```

13. All the vowels
```sql
SELECT name
   FROM world
WHERE name NOT LIKE '% %' 
AND name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
```