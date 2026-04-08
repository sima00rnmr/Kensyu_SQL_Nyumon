SELECT 口座番号,名義,種別,残高,更新日
FROM 口座 

SELECT 口座番号 FROM 口座

SELECT 口座番号,残高 FROM 口座

SELECT * FROM 口座

UPDATE 口座
SET 名義 = 'XXXXX'

UPDATE 口座
SET 残高 = 99999999,更新日 = '2024-03-01'

INSERT INTO 口座
VALUES('0642191','アオキ ハルカ',1,3640551,'2024-03-13')

INSERT INTO 口座
VALUES(1039410,'キノシタ リョウジ',1,259017,'2023-11-30')

INSERT INTO 口座 (口座番号,名義,種別,残高)
VALUES(1239855,'タカナシ ミツル',2,6509773)

DELETE FROM 口座

9
SELECT * FROM 口座
WHERE 口座番号 = '0037651'

SELECT * FROM 口座
WHERE 残高 > 0

SELECT * FROM 口座 
WHERE 口座番号 < '1000000'

SELECT * FROM 口座
WHERE 更新日 <= '2023-12-31'

SELECT * FROM 口座 
WHERE 残高 >= 1000000

SELECT * FROM 口座 
WHERE 種別 <> '1'

SELECT * FROM 口座 
WHERE 更新日 IS NULL

SELECT * FROM 口座 
WHERE 名義 LIKE '%ハシ%'

SELECT * FROM 口座 
WHERE 更新日 BETWEEN '2024-01-01' AND '2024-01-31'

SELECT * FROM 口座 
WHERE 種別  IN('2','3')

SELECT * FROM 口座 
WHERE 名義  IN('サカタ　リョウヘイ',
'マツモト　ミワコ','ハマダ　サトシ')

SELECT * FROM 口座 
WHERE '2023-12-30'<= 更新日
AND '2024-01-04' >= 更新日

または

SELECT * FROM 口座 
WHERE 更新日 
BETWEEN '2023-12-30' 
AND '2024-01-04'

SELECT * FROM 口座 
WHERE 残高 < 10000

SELECT * FROM 口座 
WHERE 残高 < 10000
AND 更新日 IS NOT NULL

×（２）
SELECT * FROM 口座
WHERE (口座番号 LIKE'2______')
OR (名義 LIKE 'エ__　%コ')

SELECT * FROM 口座
ORDER BY 口座番号

SELECT DISTINCT 名義
FROM 口座
ORDER BY 名義

SELECT 口座番号,名義,種別,残高,更新日
FROM 口座
ORDER BY 4 DESC,1

SELECT 更新日
FROM 口座
WHERE 更新日 IS NOT NULL
ORDER BY 更新日
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY

SELECT 残高,更新日
FROM 口座
WHERE 更新日 IS NOT NULL
AND 残高 > 0
ORDER BY 残高 ,更新日 DESC
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY

SELECT 口座番号
FROM 口座
UNION
SELECT 口座番号
FROM 廃止口座
ORDER BY 1

SELECT 口座番号
FROM 口座
EXCEPT
SELECT 口座番号
FROM 廃止口座
ORDER BY 1 DESC

SELECT 口座番号
FROM 口座
INTERSECT
SELECT 口座番号
FROM 廃止口座
ORDER BY 1 

SELECT 口座番号,残高
FROM 口座
WHERE 残高 = 0
UNION
SELECT 口座番号,解約時残高
FROM 廃止口座
WHERE 解約時残高 > 0
ORDER BY 1 

SELECT 口座番号,名義,'〇' AS 口座区分
FROM 口座
UNION
SELECT 口座番号,名義,'×' AS 口座区分
FROM 廃止口座
ORDER BY 2 

SELECT 口座番号,
TRUNC(残高,-3) AS 千円単位の残高
FROM 口座
WHERE 残高 >1000000

INSERT INTO 口座 (口座番号,名義,種別,残高,更新日)
VALUES ('0652281','タカギ　ノブオ','1',100000 + 3000,'2024-04-01');

INSERT INTO 口座 (口座番号,名義,種別,残高,更新日)
VALUES('1026413','マツモト　サワコ','1',300000 + 3000,'2024-04-02');

INSERT INTO 口座 (口座番号,名義,種別,残高,更新日)
VALUES('2239710','ササキ　シゲノリ','1',1000000 + 3000,'2024-04-03');

UPDATE 口座
SET (残高 -3000)*1.003
WHERE 口座番号 IN ('0652281','1026413','2239710')

37
SELECT 口座番号,更新日,
更新日+180 AS 通帳期限日
FROM 口座
WHERE 更新日 <= '2022-12-31'
厳密には < '2023-01-01' （12/31の0:00以降がカウントされない可能性）

38
SELECT 口座番号,'カ)' || 名義
FROM 口座
WHERE 種別 = '3'

39
SELECT DISTINCT 種別　AS 種別コード,
CASE 種別
WHEN '1' THEN '普通'
WHEN '2' THEN '当座'
WHEN '3' THEN '別段'
END AS 種別名
FROM 口座

SELECT 口座番号,名義,
CASE 
WHEN 残高 < 100000 THEN 'C'
WHEN 残高 BETWEEN 100000 AND 999999 THEN 'B'
ELSE 'A' END
AS 残高ランク 
FROM 口座

SELECT LENGTH(口座番号),
LENGTH(REPLACE(名義,'　','')),
LENGTH(CAST(残高 AS VARCHAR))
FROM 口座

SELECT *
FROM 口座
WHERE SUBSTRING(名義,1,5) LIKE '%カワ%'

43やり直し！！！！！





