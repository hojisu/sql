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

4. ~~~sql
   SELECT name, population
   FROM world
   WHERE population > (SELECT population FROM world WHERE name = 'Canada') AND
   population < (SELECT population FROM world WHERE name = 'Poland')
   ~~~

5. ~~~sql
   SELECT name, CONCAT(ROUND(100*population/(SELECT population FROM world WHERE name = 'Germany'), 0), '%')
   FROM world 
   WHERE continent = 'Europe' 
   ~~~

6. ~~~sql
   SELECT continent, name, area FROM world x
     WHERE area >= ALL
       (SELECT area FROM world y
           WHERE y.continent=x.continent
             AND population>0)
   ~~~

7. ~~~sql
   SELECT DISTINCT(continent), (SELECT name FROM world y WHERE y.continent = x.continent LIMIT 1) as name
   FROM world x
   ~~~

8. ~~~sql
   SELECT DISTINCT(continent), (SELECT name FROM world y WHERE y.continent = x.continent LIMIT 1) as name
   FROM world x
   ~~~

9. ~~~sql
   SELECT name, continent, population
   FROM world x
   WHERE 25000000 >= ALL(SELECT population FROM world y WHERE x.continent = y.continent and y.population > 0)
   ~~~

10. ~~~sql
    SELECT name, continent
    FROM world x
    WHERE population >= ALL(SELECT population * 3 FROM world y WHERE x.continent = y.continent and 
    x.name != y.name)
    ~~~

## SUM and COUNT

1. ~~~sql
   SELECT SUM(population)
   FROM world
   ~~~

2. ~~~sql
   SELECT DISTINCT(continent)
   FROM world
   ~~~

3. ~~~sql
   SELECT SUM(gdp)
   FROM world
   WHERE continent = 'Africa'
   ~~~

4. ~~~sql
   SELECT COUNT(area)
   FROM world
   WHERE area >= 1000000
   ~~~

5. ~~~sql
   SELECT SUM(population)
   FROM world
   WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
   ~~~

6. ~~~sql
   SELECT continent, COUNT(name)
   FROM world
   GROUP by continent 
   ~~~

7. ~~~sql
   SELECT DISTINCT(continent), COUNT(name)
   FROM world
   WHERE population > 10000000
   GROUP by continent
   ~~~

8. ~~~sql
   SELECT continent
   FROM world
   GROUP by continent
   HAVING SUM(population) >= 100000000
   ~~~

## The JOIN operation

1. ~~~sql
   SELECT matchid, player FROM goal 
     WHERE teamid= 'GER'
   ~~~

2. ~~~sql
   SELECT id, stadium, team1, team2
   FROM game
   WHERE id = 1012
   ~~~

3. ~~~sql
   SELECT player, teamid, stadium, mdate
   FROM game JOIN goal ON (id=matchid)
   WHERE teamid = 'GER'
   ~~~

4. ~~~sql
   SELECT game.team1, game.team2, goal.player
   FROM game
   JOIN goal
   ON game.id = goal.matchid
   WHERE goal.player LIKE 'Mario%'
   ~~~

5. ~~~sql
   SELECT player, teamid, coach, gtime
   FROM goal
   JOIN eteam
   ON goal.teamid = eteam.id 
   WHERE gtime<=10
   ~~~

6. ~~~sql
   SELECT game.mdate, eteam.teamname
   FROM eteam
   JOIN game
   on game.team1 = eteam.id
   WHERE eteam.coach = 'Fernando Santos'
   ~~~

7. ~~~spq
   SELECT player
   FROM game
   JOIN goal
   on game.id = goal.matchid
   WHERE game.stadium = 'National Stadium, Warsaw'
   ~~~

8. ~~~sql
   # <> against !! 
   SELECT player
     FROM game JOIN goal ON matchid = id 
       WHERE (team1='GER' or team2='GRE') and teamid <> 'GER'
   ~~~

9. ~~~sql
   SELECT teamname, COUNT(teamid)
   FROM eteam JOIN goal ON id=teamid
   GROUP BY teamname
   ~~~

10. ~~~sql
    SELECT stadium, COUNT(teamid)
    FROM goal
    JOIN game
    ON goal.matchid = game.id
    GROUP BY stadium
    ~~~

11. ~~~sql
    SELECT matchid, mdate, COUNT(teamid)
    FROM game JOIN goal ON matchid = id 
    WHERE (team1 = 'POL' OR team2 = 'POL')
    GROUP BY matchid
    ~~~

12. ~~~sql
    SELECT matchid, mdate, COUNT(teamid)
    FROM game
    JOIN goal
    ON game.id = goal.matchid
    WHERE goal.teamid = 'GER'
    GROUP BY game.id
    ~~~

## More JOIN operations

1. ~~~sql
   SELECT id, title
    FROM movie
    WHERE yr=1962
   ~~~

2. ~~~sql
   SELECT yr
   FROM movie
   WHERE title = 'Citizen Kane'
   ~~~

3. ~~~sql
   SELECT id, title, yr
   FROM movie
   WHERE title Like '%Star Trek%'
   ORDER BY yr
   ~~~

4. ~~~sql
   SELECT id
   FROM actor
   WHERE name = 'Glenn Close'
   ~~~

5. ~~~sql
   SELECT id
   FROM movie
   WHERE title = 'Casablanca'
   ~~~

6. ~~~sql
   SELECT name
   FROM actor
   JOIN casting
   ON actor.id = casting.actorid
   WHERE casting.movieid=11768
   ~~~

7. ~~~sql
   SELECT name
   FROM casting
   JOIN actor 
   ON casting.actorid = actor.id
   JOIN movie
   ON movie.id = casting.movieid
   WHERE title = 'Alien'
   ~~~

8. ~~~sql
   SELECT title
   FROM casting
   JOIN actor 
   ON casting.actorid = actor.id
   JOIN movie
   ON movie.id = casting.movieid
   WHERE name = 'Harrison Ford'
   ~~~

9. ~~~sql
   SELECT title
   FROM casting
   JOIN movie
   ON movie.id = casting.movieid
   JOIN actor
   ON actor.id = casting.actorid
   WHERE name = 'Harrison Ford' AND ord != 1
   ~~~

10. ~~~sql
    SELECT title, name
    FROM casting
    JOIN movie
    ON movie.id = casting.movieid
    JOIN actor
    ON actor.id = casting.actorid
    WHERE yr = 1962 AND ord = 1
    ~~~

11. ~~~sql
    SELECT yr,COUNT(title) FROM
      movie JOIN casting ON movie.id=movieid
            JOIN actor   ON actorid=actor.id
    WHERE name='Rock Hudson'
    GROUP BY yr
    HAVING COUNT(title) > 2
    ~~~

12. 

