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

SELECT  *
FROM 口座
WHERE LENGTH(CAST(残高 AS VARCHAR)) > 4
AND SUBSTRING(CAST(残高 AS VARCHAR),(LENGTH(CAST(残高 AS VARCHAR))-2),3) = '000'


SELECT *
FROM 口座
WHERE LENGTH(CAST(残高 AS VARCHAR)) >= 4
AND SUBSTRING(CAST(残高 AS VARCHAR),LENGTH(CAST(残高 AS VARCHAR))-2,3) = '000'

SELECT 口座番号,残高,
TRUNC(残高*0.0002,0) AS 利息
FROM 口座
ORDER BY 残高 DESC

SELECT 口座番号,残高,
CASE 
WHEN 残高 < 500000 THEN TRUNC(残高*0.0001,0)
WHEN 残高 BETWEEN 500000 AND 1999999 THEN TRUNC(残高*0.0002,0)
WHEN 残高 >= 2000000 THEN TRUNC(残高*0.0003,0)
END AS 残高別利息
FROM 口座
ORDER BY 残高別利息 DESC,口座番号

INSERT INTO 口座
VALUES('0351262','イトカワ　ダイ','2',635110,CURRENT_DATE);
INSERT INTO 口座
VALUES('1015513','アサツ　ジュンジ','1',88463,CURRENT_DATE);
INSERT INTO 口座
VALUES('1739298','ホシノ　サトミ','1',704610,CURRENT_DATE);

SELECT 口座番号,名義,種別,残高,
SUBSTRING(CAST(更新日 AS VARCHAR),1,4)||
'年' ||
SUBSTRING(CAST(更新日 AS VARCHAR),6,2)||
'月' ||
SUBSTRING(CAST(更新日 AS VARCHAR),9,2)||
'日' 
FROM 口座
WHERE 更新日 >= '2024-01-01'

SELECT 
COALESCE (CAST(更新日 AS VARCHAR) , '設定なし')
AS 更新日
FROM 口座

SELECT SUM(残高),MAX(残高),
MIN(残高),AVG(残高),COUNT(残高)
FROM 口座

SELECT COUNT(*) AS 件数
FROM 口座
WHERE 種別 <> '1' 
AND 残高 >= 1000000 
AND 更新日 < '2024-01-01'

SELECT COUNT(*)-COUNT(更新日) AS 件数
FROM 口座

SELECT MAX(名義),MIN(名義) FROM 口座

SELECT MAX(更新日) AS 新しい日付,
MIN(更新日)AS 古い日付
FROM 口座

SELECT 種別,SUM(残高) AS 合計,MAX(残高) AS 最大,
MIN(残高) AS 最小,AVG(残高) AS 平均 
,COUNT(口座番号) AS 件数
FROM 口座
GROUP BY 種別

SELECT SUBSTRING(口座番号,7,1) 
AS 口座番号下1桁,
COUNT(口座番号) AS 件数
FROM 口座
GROUP BY SUBSTRING(口座番号,7,1)
ORDER BY 件数 DESC

SELECT SUBSTRING(COALESCE(CAST(更新日 AS VARCHAR),'XXXX'),1,4),
SUM(残高)AS 合計,
MAX (残高)AS 最大,
MIN (残高)AS 最小,
AVG (残高) AS 平均,
COUNT (口座番号) AS 登録件数
FROM 口座
GROUP BY SUBSTRING(COALESCE(CAST(更新日 AS VARCHAR),'XXXX'),1,4)
ORDER BY COUNT (口座番号) DESC

SELECT 種別,SUM(残高),COUNT(*)　
FROM 口座
GROUP BY 種別
HAVING SUM(残高) > 3000000

SELECT SUBSTRING(名義,1,1) AS 名義,COUNT(名義) AS 件数,
AVG(LENGTH(REPLACE(名義,'　',''))) AS 文字数の平均
FROM 口座
GROUP BY SUBSTRING(名義,1,1)
HAVING AVG(LENGTH(REPLACE(名義,'　',''))) >= 5 
OR COUNT(名義)>=10

SELECT 残高,
(SELECT SUM(入金額) FROM 取引 
WHERE 日付 = '2023-12-28' AND 口座番号 = '1115600') AS 入金額,
(SELECT SUM(出金額) FROM 取引 
WHERE 日付 = '2023-12-28' AND 口座番号 = '1115600') AS 出金額
FROM 口座
WHERE 更新日 = '2023-12-28' AND 口座番号 = '1115600'

※60のおまけ…JOIN使った文（問題文では　副問い合わせでSELECT使えと記載があるので今回は不適）
SELECT k.残高,
COALESCE(SUM(t.入金額),0) AS 入金額合計,
COALESCE(SUM(t.出金額),0) AS 出金額合計
FROM 口座 k
LEFT JOIN 取引 t
ON k.口座番号 = t.口座番号
AND t.日付 = '2023-12-28'
WHERE k.口座番号 = '1115600'
GROUP BY k.残高
 

SELECT 口座番号,名義,残高
FROM 口座
WHERE 口座番号 IN (SELECT 口座番号
FROM 取引 
WHERE 入金額>1000000 OR 出金額>1000000)

SELECT * FROM 口座
WHERE 更新日 > ALL(SELECT 日付 FROM 取引)

SELECT K.口座番号,K.名義,K.残高,T.日付,T.入金額,T.出金額
FROM 口座 AS K
JOIN 取引 AS T
ON K.口座番号=T.口座番号
WHERE K.口座番号 = '0887132'
ORDER BY T.取引番号 

※※※　確認
自分の回答
SELECT T.口座番号,K.名義,K.残高
FROM 口座 AS K
JOIN 取引 AS T
ON K.口座番号=T.口座番号
WHERE T.日付 = '2022-03-01'
EXCEPT 
SELECT 口座番号,名義,解約時残高 FROM 廃止口座

模範解答（これだと除外してなくない…？）
SELECT T.口座番号,K.名義,K.残高 
FROM 取引 AS T 
JOIN 口座 AS K
ON T.口座番号 = K.口座番号
WHERE T.日付 ='2022-03-01'
→自分の日本語理解の問題かもしれない…解決

SELECT T.口座番号,
COALESCE(K.名義,'解約済み') AS 名義,
COALESCE(K.残高,0) AS 残高
FROM 取引 AS T
JOIN 口座 AS K
ON T.口座番号 = K.口座番号
WHERE T.日付 = '2022-03-01'

SELECT T.取引番号,
CAST(Y.取引事由id AS VARCHAR) || ':' || Y.取引事由名 AS 取引事由,
T.日付,T.口座番号,T.入金額,T.出金額
FROM 取引 AS T
RIGHT JOIN 取引事由 AS Y
ON T.取引事由id = Y.取引事由id

SELECT DISTINCT COALESCE(T.取引事由id,Y.取引事由id),Y.取引事由名
FROM 取引 AS T 
FULL JOIN 取引事由 AS Y 
ON T.取引事由id = Y.取引事由id

71 70を抜かしてる、このあとやる
SELECT K.口座番号,K.名義,K.残高,T.日付,Y.取引事由名,T.入金額,T.出金額
FROM 口座 AS K
JOIN 取引 AS T
ON K.口座番号=T.口座番号
JOIN 取引事由 AS Y
ON T.取引事由id = Y.取引事由id
WHERE K.口座番号 = '0887132'
ORDER BY T.取引番号

SELECT K.口座番号,K.名義,K.残高,
T.日付 AS 取引の日付,T.取引事由id,T.入金額,T.出金額
FROM 口座 AS K
JOIN 取引 AS T
ON K.口座番号 = T.口座番号 
WHERE K.残高 > 5000000 
AND T.日付 >= '2024-01-01' 
AND (T.入金額 > 1000000 OR T.出金額 > 1000000)

（口座テーブルを副問い合わせにした）
SELECT K.口座番号,K.名義,K.残高,
T.日付 AS 取引の日付,T.取引事由id,T.入金額,T.出金額
FROM 取引 AS T
JOIN (SELECT 口座番号,名義,残高 
FROM 口座
WHERE 残高 >= 5000000) AS K
ON T.口座番号 = K.口座番号 
WHERE T.日付 >= '2024-01-01' 
AND (T.入金額 > 1000000 OR T.出金額 > 1000000)

74 じぶんの回答
SELECT K.口座番号,T.回数,K.名義
FROM 口座 AS K
JOIN (SELECT 口座番号,COUNT(*) AS 回数 FROM 取引 
GROUP BY 口座番号,日付) T
ON K.口座番号 = T.口座番号
WHERE T.回数 >= 3

模範解答は
SELECT K.口座番号,T.回数,K.名義
FROM 口座 AS K
JOIN (SELECT 口座番号,
COUNT(*) AS 回数 FROM 取引 
GROUP BY 口座番号,日付 
HAVING T.回数 >= 3) T
ON K.口座番号 = T.口座番号

自己結合を用いた方法
SELECT K.名義,K.口座番号,K.種別,K.残高,K.更新日
FROM 口座 AS K
JOIN (SELECT 名義,COUNT(名義) AS 重複した名義 FROM 口座 GROUP BY 名義) C
ON K.名義 = C.名義
WHERE C.重複した名義 >= 2
ORDER BY K.名義 DESC, K.口座番号

ーーーーーーーーーーーーーーーーーーーーーーーーーー
SELECT 商品コード,商品名,単価,
商品区分,関連商品コード
FROM 商品

SELECT 商品名
FROM 商品

SELECT *
FROM 商品

SELECT 注文番号,注文枝番,商品コード
FROM 注文

INSERT INTO 商品(商品コード,商品名,単価,商品区分)
VALUES ('W0461','冬のあったかコート',12800,'1');

INSERT INTO 商品(商品コード,商品名,単価,商品区分)
VALUES ('S0331','春のさわやかコート',6800,'1');

INSERT INTO 商品(商品コード,商品名,単価,商品区分)
VALUES ('A0582','秋のシックなコート',9800,'1');

SELECT * FROM 商品
WHERE 商品コード = 'W1252'

UPDATE 商品
SET 単価 = 500
WHERE 商品コード = 'S0023'

SELECT * FROM 商品
WHERE 単価 <= 1000

SELECT * FROM 商品
WHERE 単価 >= 5000

SELECT * FROM 注文
WHERE 注文日 >= '2024-01-01'

SELECT * FROM 注文
WHERE 注文日 < '2023-12-01'

SELECT * FROM 商品
WHERE 商品区分 <> '1'

SELECT *
FROM 注文
WHERE クーポン割引料 IS NULL

DELETE 
FROM 商品
WHERE 商品コード LIKE 'N%'

SELECT 商品コード,商品名,単価 
FROM 商品
WHERE 商品名 LIKE '%コート%'

SELECT 商品コード,商品区分
FROM 商品
WHERE 商品区分 IN('2','3','9')

SELECT *
FROM 商品
WHERE 商品コード BETWEEN 'A0100' AND 'A0500'

SELECT * 
FROM 注文
WHERE 商品コード IN('N0501','N1021','N0223')

SELECT * 
FROM 商品
WHERE 商品区分 = '3' AND 商品名 LIKE '%水玉%'

SELECT *
FROM 商品
WHERE 商品名 LIKE '%ゆるふわ%' 
OR 商品名 LIKE '%軽い%'

SELECT 
FROM 商品
WHERE (商品区分 = '1' AND 単価 <= 3000)
OR (商品区分 = '3' AND 単価 >= 10000)

SELECT 商品コード 
FROM 注文
WHERE '024-04-01' 
AND 数量 >= 3

SELECT *
FROM 注文
WHERE 数量 >=10 
OR クーポン割引料 IS NOT NULL

SELECT 商品コード,商品名
FROM 商品
WHERE 商品区分 = '1'
ORDER BY 商品コード DESC

SELECT 注文日,注文番号,注文枝番,商品コード,数量
FROM 注文
WHERE 注文日 >= '2024-03-01'
ORDER BY 注文日,注文番号,注文枝番

SELECT DISTINCT 商品コード 
FROM 注文
ORDER BY 商品コード

SELECT DISTINCT 商品コード 
FROM 注文
ORDER BY 商品コード

SELECT *
FROM 商品
ORDER BY 単価 
OFFSET 5 ROWS
FETCH NEXT 15 ROWS ONLY

SELECT *
FROM 廃番商品
WHERE 売上個数 >= 100
UNION
SELECT *
FROM 廃番商品
WHERE 廃番日 >= '2022-12-01' 
AND 廃番日 < '2023-01-01'
ORDER BY 売上個数 DESC

(自分のコード
UNIONを使わない
SELECT * 
FROM 廃番商品 
WHERE 売上個数 >= 100 
OR (廃番日 >= '2022-12-01' AND 廃番日 < '2023-01-01') 
ORDER BY 売上個数 DESC
…ダメかなあ？)

SELECT 商品コード
FROM 商品
EXCEPT
SELECT 商品コード
FROM 注文
ORDER BY 1

SELECT 商品コード
FROM 商品
INTERSECT
SELECT 商品コード
FROM 注文
ORDER BY 1 DESC

SELECT 商品コード,商品名,単価
FROM 商品
WHERE 商品区分= '9' 
AND 単価 >=10000
UNION
SELECT 商品コード,商品名,単価
FROM 商品
WHERE 商品区分= '9'
AND 単価 <= 1000
ORDER BY 3,1

SELECT 商品コード,単価,単価*0.95 AS キャンペーン価格
FROM 商品
WHERE 商品区分 = '9'
ORDER BY 商品コード

UPDATE 注文
SET クーポン割引料 = クーポン割引料 + 300
WHERE 注文日 >= '2024-03-12' 
AND 注文日 < '2024-03-15' 
AND クーポン割引料 IS NOT NULL
AND 数量 >= 2

UPDATE 注文
SET 数量 = 数量-1
WHERE 商品コード = 'W0156' 
AND 注文番号 = '202402250126' 

37　自分のコード（！脆弱）
SELECT 注文日,
注文番号 || '-' || 注文枝番 AS 注文番号,
商品コード,数量,クーポン割引料
FROM 注文
WHERE 注文番号 
BETWEEN '202310010001' AND '202310319999' 

模範解答
SELECT 注文日,
注文番号 || '-' || CAST(注文枝番 AS VARCHAR) AS 注文番号,
商品コード,数量,クーポン割引料
FROM 注文
WHERE 注文番号 >= '202310010001'
AND 注文番号 <= '202310319999'
ーーーーーーーーーーーーーーー




