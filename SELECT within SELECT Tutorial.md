# SELECT within SELECT Tutorial

1. Bigger than Russia
List each country name where the population is larger than that of 'Russia'.
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

2. Richer than UK
Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql
SELECT name FROM world
WHERE continent='Europe' and gdp/population> (SELECT gdp/population FROM world
WHERE name= 'United Kingdom')
```

3. Neighbours of Argentina and Australia
List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql
SELECT name, continent FROM world
WHERE continent IN (SELECT continent FROM world
WHERE name IN ('Argentina', 'Australia'))
ORDER BY name
```

4. Between Canada and Poland
Which country has a population that is more than Canada but less than Poland? Show the name and the population.
```sql
SELECT name, population FROM world
WHERE population > (SELECT population FROM world where name ='Canada') and population < (SELECT population FROM world where name ='Poland')
```

5. Percentages of Germany
Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```sql
SELECT name, CONCAT(ROUND((population/(SELECT population FROM world WHERE name= 'Germany'))*100),'%') FROM world
WHERE continent='Europe'
```

6. Bigger than every country in Europe
Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)
```sql
SELECT name FROM world
WHERE gdp> (SELECT MAX(gdp) FROM world
WHERE continent= 'Europe')
```

7. Largest in each continent
Find the largest country (by area) in each continent, show the continent, the name and the area:
```sql
SELECT continent, name, area FROM world x
  WHERE area=
    (SELECT MAX(area) FROM world y
        WHERE y.continent=x.continent)
```

8. First country of each continent (alphabetically)
List each continent and the name of the country that comes first alphabetically.
```sql
SELECT continent, name FROM world x
WHERE name = (SELECT name FROM world y
WHERE y.continent= x.continent
ORDER BY name
LIMIT 1)
```

9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.
```sql
SELECT name, continent, population FROM world x
WHERE 25000000 > ALL (SELECT population FROM world z
WHERE z.continent= x.continent)
 ```
 
 10. Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.
```sql
SELECT name, continent FROM world x
WHERE x.population > (SELECT 3* population FROM world y
WHERE y.continent= x.continent and y.name <> x.name
ORDER BY population DESC
LIMIT 1)
```