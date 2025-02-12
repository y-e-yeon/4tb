## 1. 우리 플랫폼에 정착한 판매자[🔗](https://solvesql.com/problems/settled-sellers-1/)

```SQL
SELECT
  seller_id,
  COUNT(DISTINCT order_id) AS orders
FROM olist_order_items_dataset
GROUP BY
  seller_id
HAVING
  orders >= 100
ORDER BY orders DESC;
```

## 2. 몇 분이서 오셨어요?[🔗](https://solvesql.com/problems/size-of-table/)

```SQL
SELECT
  *
FROM tips
WHERE
  MOD(size,2) = 1;
```

## 3. 최고의 근무일을 찾아라[🔗](https://solvesql.com/problems/best-working-day/)

```SQL
SELECT
  day,
  SUM(tip) AS tip_daily
FROM tips
GROUP BY
  day
ORDER BY tip_daily DESC
LIMIT 1;
```

## 4. Group by, Join, Having 사용[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/164668)

```SQL
SELECT
    USED_GOODS_USER.USER_ID,
    USED_GOODS_USER.NICKNAME,
    SUM(USED_GOODS_BOARD.PRICE) AS TOTAL_SALES
FROM USED_GOODS_BOARD
INNER JOIN USED_GOODS_USER
ON USED_GOODS_BOARD.WRITER_ID = USED_GOODS_USER.USER_ID
WHERE
    USED_GOODS_BOARD.STATUS = "DONE"
GROUP BY
    USED_GOODS_BOARD.WRITER_ID, USED_GOODS_USER.USER_ID
HAVING
    TOTAL_SALES >= 700000
ORDER BY TOTAL_SALES ASC
```

## 5. WINDOW[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/273712)

```SQL
SELECT
    I.ITEM_ID,
    I.ITEM_NAME,
    I.RARITY
FROM ITEM_INFO AS I
LEFT JOIN ITEM_TREE AS T
ON I.ITEM_ID = T.PARENT_ITEM_ID
WHERE T.PARENT_ITEM_ID IS NULL
ORDER BY ITEM_ID DESC
```

## 6. JOIN[🔗](https://school.programmers.co.kr/learn/courses/30/lessons/276034)

```SQL
SELECT
    D.ID,
    D.EMAIL,
    D.FIRST_NAME,
    D.LAST_NAME
FROM
    DEVELOPERS AS D
JOIN SKILLCODES AS S
ON (D.SKILL_CODE & S.CODE) = S.CODE
WHERE
    S.NAME IN ('Python', 'C#')
ORDER BY
    D.ID ASC;
```