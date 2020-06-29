[SQLZOO solution]

## SELECT basics

1. ~~~sql
   select population
   from world
   where name = 'Germany'
   ~~~

2. ~~~sql
   select name, population
   from world
   where name in ('Sweden', 'Norway', 'Denmark')
   ~~~

3. ~~~sql
   select name, area
   from world
   where area between 200000 and 250000
   ~~~

## SELECT from WORLD Tutorial

1. ~~~sql
   SELECT name, continent, population 
   FROM world
   ~~~

2. ~~~sql
   SELECT name FROM world
   WHERE population > 200000000
   ~~~

3. ~~~sql
   select name, GDP/population
   from world
   where population > 200000000
   ~~~

4. ~~~sql
   select name, population/1000000
   from world
   where continent = 'South America'
   ~~~

5. ~~~sql
   select name, population
   from world
   where name in ('France', 'Germany', 'Italy')
   ~~~

6. ~~~sql
   select name
   from world
   where name like '%United%'
   ~~~

7. ~~~sql
   select name, population, area
   from world
   where area > 3000000 or population > 250000000
   ~~~

8. ~~~sql
   # One or the other (but not both) => XOR
   
   select name, population, area
   from world
   where area > 3000000 xor population > 250000000
   ~~~

9. ~~~sql
   select name, round(population/1000000, 2), round(GDP/1000000000, 2)
   from world
   where continent = 'South America'
   ~~~

10. ~~~sql
    select name, round(gdp/population, -3)
    from world
    where gdp > 1000000000000
    ~~~

11. ~~~sql
    SELECT name, capital
    FROM world
    WHERE LENGTH(name) = LENGTH(capital)
    ~~~

12. ~~~sql
    # `<>` not equals
    SELECT name, capital
    FROM world
    where left(name, 1) = left(capital, 1) and name <> capital
    ~~~

13. ~~~sql
    SELECT name
       FROM world
    WHERE name LIKE '%a%' 
    and name LIKE '%e%' 
    and name LIKE '%i%' 
    and name LIKE '%o%' 
    and name LIKE '%u%'
    and name NOT LIKE '% %'
    ~~~

14. 

