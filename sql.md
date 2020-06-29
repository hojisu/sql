## 프로그래머스 SQL 문제 풀이

- 역순정렬하기

~~~sql
SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC
~~~

- 아픈 동물 찾기

~~~sql
SELECT animal_id, name
from animal_ins
where intake_condition = 'Sick'
~~~

- 어린 동물 찾기

~~~sql
SELECT animal_id, name
from animal_ins
where intake_condition != 'Aged'
~~~

- 동물의 아이디어와 이름

~~~sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
~~~

- 여러기준으로 정렬하기

~~~sql
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC
~~~

- 상위 N개의 코드

~~~sql
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME 
LIMIT 1	
~~~

- 고양이와 개는 몇 마리 일까

~~~sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) as count
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE
~~~

- 동명 동물 수 찾기

~~~sql
SELECT NAME, COUNT(NAME) as COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) >= 2
ORDER BY NAME
~~~

- 입양시간구하기(1)

보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

~~~sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) as COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >= 9 AND HOUR(DATETIME) <= 19
GROUP BY HOUR(DATETIME)
ORDER BY HOUR(DATETIME) 
~~~

