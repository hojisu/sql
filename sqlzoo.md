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

## SELECT from Nobel Tutorial

1. ~~~sql
   SELECT yr, subject, winner
     FROM nobel
    WHERE yr = 1950
   ~~~

2. ~~~sql
   SELECT winner
     FROM nobel
    WHERE yr = 1962
      AND subject = 'Literature'
   ~~~

3. ~~~sql
   select yr, subject
   from nobel
   where winner = 'Albert Einstein'
   ~~~

4. ~~~sql
   select winner
   from nobel
   where yr >= 2000 and subject like '%Peace%'
   ~~~

5. ~~~sql
   select yr, subject, winner
   from nobel
   where subject = 'Literature' and yr between '1980' and '1989'
   ~~~

6. ~~~sql
   SELECT * FROM nobel
   WHERE winner IN ('Theodore Roosevelt',
                     'Woodrow Wilson',
                     'Jimmy Carter', 
                     'Barack Obama')
   ~~~

7. ~~~sql
   select winner
   from nobel
   where winner like 'John%'
   ~~~

8. ~~~sql
   select yr, subject, winner
   from nobel
   where subject = 'Physics' and yr = '1980' or 
         subject = 'Chemistry' and yr = '1984'
   ~~~

9. ~~~sql
   select *
   from nobel
   where yr = 1980 and subject not in ('Chemistry', 'Medicine')
   ~~~

10. ~~~sql
    select *
    from nobel
    where subject = 'Medicine' and yr < 1910 or subject = 'Literature' and yr >= 2004
    ~~~

11. ~~~sql
    select *
    from nobel
    where winner = 'PETER GRÜNBERG'
    ~~~

12. ~~~sql
    select *
    from nobel
    where winner = "EUGENE O'NEILL"
    ~~~

13. ~~~sql
    select winner, yr, subject
    from nobel
    where winner like 'Sir%'
    order by yr DESC, winner
    ~~~

14. ~~~sql
    SELECT winner, subject
      FROM nobel
     WHERE yr=1984
     ORDER BY 
     CASE WHEN subject IN ('Physics','Chemistry') THEN 1 ELSE 0 END, subject, winner
    ~~~

## SELECT within SELECT Tutorial

1. ~~~sql
   SELECT name FROM world
     WHERE population >
        (SELECT population FROM world
         WHERE name='Russia')
   ~~~

2. ~~~sql
   SELECT name
   FROM world
   WHERE continent = 'Europe' 
   AND gdp/population > (SELECT gdp/population FROM world WHERE name = 'United Kingdom')
   ~~~

3. ~~~sql
   SELECT name, continent
   FROM world
   WHERE continent = (SELECT continent FROM world WHERE name = 'Argentina') OR
   continent = (SELECT continent FROM world WHERE name = 'Australia') 
   ORDER BY name
   ~~~

4. 

