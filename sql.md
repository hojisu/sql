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

- 없어진 기록 찾기

~~~sql
SELECT ANIMAL_OUTS.ANIMAL_ID, ANIMAL_OUTS.NAME
FROM ANIMAL_OUTS
LEFT JOIN ANIMAL_INS
ON ANIMAL_OUTS.ANIMAL_ID = ANIMAL_INS.ANIMAL_ID
WHERE ANIMAL_INS.ANIMAL_ID IS NULL
ORDER BY ANIMAL_OUTS.ANIMAL_ID
~~~

- 있었는데요 없었습니다.

관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일이 빠른 순으로 조회해야합니다.

~~~sql
SELECT I.ANIMAL_ID, I.NAME
FROM ANIMAL_INS I
LEFT JOIN ANIMAL_OUTS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.DATETIME > O.DATETIME
ORDER BY I.DATETIME 
~~~

- 오랜 기간 보호한 동물(1)

아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일 순으로 조회해야 합니다.

~~~sql
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS I
LEFT JOIN ANIMAL_OUTS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE O.ANIMAL_ID IS NULL
ORDER BY I.DATETIME
LIMIT 3		
~~~

- 보호소에서 중성화한 동물

보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화[1](https://programmers.co.kr/learn/courses/30/lessons/59045#fn1)되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.

~~~sql
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS I
JOIN ANIMAL_OUTS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE != O.SEX_UPON_OUTCOME
ORDER BY ANIMAL_ID
~~~

- 루시와 엘라 찾기

동물 보호소에 들어온 동물 중 이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물의 아이디와 이름, 성별 및 중성화 여부를 조회하는 SQL 문을 작성해주세요.

~~~sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS 
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
~~~

- 이름에 el이 들어가는 동물 찾기

보호소에 돌아가신 할머니가 기르던 개를 찾는 사람이 찾아왔습니다. 이 사람이 말하길 할머니가 기르던 개는 이름에 'el'이 들어간다고 합니다. 동물 보호소에 들어온 동물 이름 중, 이름에 EL이 들어가는 개의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 이름 순으로 조회해주세요. 단, 이름의 대소문자는 구분하지 않습니다.

~~~sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE NAME LIKE '%el%' AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME
~~~

- 중성화 여부 파악하기

보호소의 동물이 중성화되었는지 아닌지 파악하려 합니다. 중성화된 동물은 `SEX_UPON_INTAKE` 컬럼에 'Neutered' 또는 'Spayed'라는 단어가 들어있습니다. 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시해주세요.

~~~sql
SELECT ANIMAL_ID, NAME, 
       CASE WHEN SEX_UPON_INTAKE LIKE '%Neutered%' OR SEX_UPON_INTAKE LIKE '%Spayed%' THEN 'O' ELSE 'X' 
       END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
~~~

- 오랜 기간 보호한 동물(2)

입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 기간이 긴 순으로 조회해야 합니다.

~~~sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_OUTS O
LEFT JOIN ANIMAL_INS I
ON O.ANIMAL_ID = I.ANIMAL_ID
ORDER BY O.DATETIME - I.DATETIME DESC
LIMIT 2
~~~

- ATETIME에서 DATE로 형 변환

`ANIMAL_INS` 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜[1](https://programmers.co.kr/learn/courses/30/lessons/59414#fn1)를 조회하는 SQL문을 작성해주세요. 이때 결과는 아이디 순으로 조회해야 합니다.

~~~sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d')
FROM ANIMAL_INS
~~~

- 이름이 없는 동물의 아이디

동물 보호소에 들어온 동물 중, 이름이 없는 채로 들어온 동물의 ID를 조회하는 SQL 문을 작성해주세요. 단, ID는 오름차순 정렬되어야 합니다.

~~~sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME is NULL
~~~

- 이름이 있는 동물의 아이디

동물 보호소에 들어온 동물 중, 이름이 있는 동물의 ID를 조회하는 SQL 문을 작성해주세요. 단, ID는 오름차순 정렬되어야 합니다.

~~~sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME is NOT NULL	
~~~

- NULL 처리하기

입양 게시판에 동물 정보를 게시하려 합니다. 동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 No name으로 표시해 주세요.

~~~sql
SELECT ANIMAL_TYPE, IFNULL(NAME, "No name") as NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
~~~

