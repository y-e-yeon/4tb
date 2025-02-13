# Advanced - 6주차
## 1. 틀린 코드 이유 분석

#### 틀린 코드

```SQL
SELECT *
FROM (SELECT FOOD_TYPE, REST_ID, REST_NAME, MAX(FAVORITES) AS FAVORITES
FROM REST_INFO
GROUP BY FOOD_TYPE
ORDER BY FOOD_TYPE DESC
```
이 코드가 틀린 이유를 찾아내고, 정답 코드와 비교해 정리해주세요.

#### 정답 코드

```SQL
SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM REST_INFO
WHERE (FOOD_TYPE, FAVORITES) IN (
    SELECT FOOD_TYPE, MAX(FAVORITES)    
    FROM REST_INFO
    GROUP BY FOOD_TYPE
) 
ORDER BY FOOD_TYPE DESC;
```

또한, 이 문제에서는 아래 **개선된 쿼리**로도 조회될 수 있습니다. 

**ROW_NUMBER 윈도우 함수**를 사용합니다.

## 2. 개선된 쿼리 학습

#### 개선된 쿼리

```SQL
WITH RankedRest AS (
    SELECT 
        FOOD_TYPE, REST_ID, REST_NAME, FAVORITES,
        ROW_NUMBER() OVER (PARTITION BY FOOD_TYPE ORDER BY FAVORITES DESC, REST_ID) AS rnk
    FROM REST_INFO
)
SELECT 
    FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM RankedRest
WHERE rnk = 1
ORDER BY FOOD_TYPE DESC;
```

이 코드를 단계별로 해석하고(주석 사용 등), 위 코드에 비해 갖는 이점을 설명하세요.

## 3. [SUBQUERY] 조건에 맞는 사원 정보 조회하기[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/284527)


기본 코드
```SQL
SELECT 
    EMP_NO, 
    EMP_NAME, 
    SAL,
    RANK() OVER (ORDER BY SAL DESC) AS rnk
FROM 
    HR_EMPLOYEES;
```

이때, RANK(), DENSE_RANK(), ROW_NUMBER() 함수를 사용하며 결과를 비교하고 해당 함수를 사용하는 경우를 서술해주세요. (함수 사용 예제는 직접 찾아보기)

# Advanced - 7주차
## [ISNULL] NULL처리하기 (SQL 고득점kit)[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/59410)

**동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성합니다.**

이때, 이름이 없는 동물의 이름은 ‘No name’으로 합니다.

### 문제1. IFNULL()으로 해결

같은 문제를, CASE WHEN 문법을 사용하여 해결해주세요
문제2. CASE WHEN으로 해결

## 중성화 여부 파악하기[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/59409#qna)

### 문제 3. 문제를 풀어주세요 (힌트: IF, LIKE를 사용할 수 있습니다)

### 문제 4. 아래는 QnA에 올라온 질문입니다. 왜 풀이가 틀렸는지 답해주세요.[🔗](https://school.programmers.co.kr/questions/80270)

# 린터 문제
## 1. [JOIN] 있었는데요 없었습니다[🔗]
1. [JOIN](https://school.programmers.co.kr/learn/courses/30/parts/17046)/ **있었는데요 없었습니다**
    
    https://school.programmers.co.kr/learn/courses/30/lessons/59043
    
2. [GROUP BY](https://school.programmers.co.kr/learn/courses/30/parts/17044)/**고양이와 개는 몇 마리 있을까**

http://school.programmers.co.kr/learn/courses/30/lessons/59040 

1. [SELECT](https://school.programmers.co.kr/learn/courses/30/parts/17042)/ **특정 세대의 대장균 찾기**

https://school.programmers.co.kr/learn/courses/30/lessons/301650

1. **SUBQUERY/폐쇄할 따릉이 정류소 찾기 2**

https://solvesql.com/problems/find-unnecessary-station-2/