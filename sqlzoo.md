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

4. 