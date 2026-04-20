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
FROM 廃止口座SE
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

44
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

UPDATE 口座
SET 残高 = (SELECT SUM(COALESCE(入金額,0)) - SUM(COALESCE(出金額,0)) FROM 取引 
WHERE 口座番号 ='0351333' AND 更新日 = '2024-01-11'),
更新日='2024-01-11'
WHERE 口座番号 ='0351333'

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
WHERE 入金額>1000000)

SELECT * FROM 口座
WHERE 更新日 > ALL(SELECT 日付 FROM 取引)

63-
SELECT A.日付,
(SELECT MAX (入金額) FROM 取引 
WHERE 口座番号 = '3104451') AS 最大入金額,
(SELECT MAX (出金額) FROM 取引 
WHERE 口座番号 = '3104451') AS 最大出金額
FROM (SELECT 日付 FROM 取引 WHERE 口座番号 = '3104451'
GROUP BY 日付
HAVING SUM(入金額) >0 AND SUM(出金額) >0

64
INSERT INTO 廃止口座
SELECT * FROM 口座 WHERE 口座番号 = '2761055';
DELETE FROM 口座
WHERE 口座番号 = '2761055'

65
SELECT T.口座番号,T.日付,Y.取引事由名,
COALESCE(T.入金額,0)-COALESCE(T.出金額,0) AS 取引金額
FROM 取引事由 AS Y
JOIN 取引 AS T
ON Y.取引事由id = T.取引事由id
WHERE T.口座番号 IN('0311240','1234161','2750902')
ORDER BY T.口座番号,T.取引番号

GROUP BY 日付
HAVING SUM(入金額) >0 AND SUM(出金額) >0) AS A

66
LECT K.口座番号,K.名義,K.残高,T.日付,T.入金額,T.出金額
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

73 ２つのやり方で
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

（取引テーブルを副問い合わせにした）
SELECT K.口座番号,K.名義,K.残高,T.日付 AS 取引の日付,
T.取引事由id,T.入金額,T.出金額
FROM 口座 AS K
JOIN (SELECT 口座番号,日付,取引事由id,入金額,出金額 FROM 取引
WHERE 日付 >= '2024-01-01' 
AND (入金額 >= 1000000 OR 出金額 >= 1000000))AS T
ON K.口座番号= T.口座番号
WHERE K.残高 >= 5000000


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
38
SELECT DISTINCT 商品区分 AS 区分,CASE 
WHEN 商品区分 = '1' THEN '衣類'
WHEN 商品区分 = '2' THEN '靴'
WHEN 商品区分 = '3' THEN '雑貨'
WHEN 商品区分 = '9' THEN '未分類'
END AS 区分名
FROM 商品

39
SELECT 商品コード,商品名,単価,CASE 
WHEN 単価 < 3000 THEN 'S'
WHEN 単価 >= 3000 AND 単価 < 10000 THEN 'M'
WHEN 単価 >= 10000 THEN 'L'
END AS 販売価格ランク,
商品区分 ||':'||  CASE
WHEN 商品区分 ='1'THEN '衣類'
WHEN 商品区分 ='2'THEN '靴'
WHEN 商品区分 ='3'THEN '雑貨'
WHEN 商品区分 ='9'THEN '未分類'
END AS 商品区分
FROM 商品
ORDER BY 単価,商品コード

SELECT 商品名,LENGTH (商品名) AS 文字数
FROM 商品
WHERE LENGTH (商品名) >= 10 
ORDER BY LENGTH (商品名)

SELECT 注文日,SUBSTRING(注文番号,9,4) AS 注文番号
FROM 注文

42
自分の回答（全部置換になるからダメ）
UPDATE 商品
SET 商品コード = REPLACE(商品コード,'M','E')
WHERE 商品コード LIKE 'M%'

模範解答
UPDATE 商品 SET 商品コード = 'E' || 
SUBSTRING(商品コード,2,4)
WHERE SUBSTRING(商品コード,1,1) ='M'

SELECT SUBSTRING(注文番号,9,4)
FROM 注文 
WHERE SUBSTRING(注文番号,9,4) >= '1000'
AND SUBSTRING(注文番号,9,4) < '2000'
ORDER BY SUBSTRING(注文番号,9,4)

UPDATE 廃番商品
SET 廃番日 = CURRENT_DATE
WHERE 商品コード = 'S1990'

SELECT TRUNC(単価*0.7,0) AS 値下げした単価,
商品コード,商品,単価 AS 現在の単価
FROM 商品
WHERE 単価 > 10000

SELECT SUM(数量) AS 数量の合計
FROM 注文

SELECT 注文日,SUM(数量) AS 数量の合計
FROM 注文
GROUP BY 注文日
ORDER BY 注文日

SELECT 商品区分,MAX(単価) AS 最高額,
MIN(単価) AS 最小額
FROM 商品
GROUP BY 商品区分
ORDER BY 商品区分

SELECT 商品コード,SUM(数量) AS 販売した数量
FROM 注文
GROUP BY 商品コード
ORDER BY 販売した数量 DESC,商品コード
OFFSET 0 ROW 
FETCH NEXT 10 ROWS ONLY

SELECT 商品コード,SUM(数量) AS 販売した数量
FROM 注文
GROUP BY 商品コード
HAVING SUM(数量) < 5 

52 COALESCEは今回不要らしい
SELECT COUNT(クーポン割引料) AS 注文件数,
SUM(COALESCE(クーポン割引料,0)) AS 割引額の合計
FROM 注文

SELECT SUBSTRING(CAST(注文番号 AS VARCHAR),1,6) AS 年月,
COUNT(*) AS 注文件数
FROM 注文
WHERE 注文枝番 = 1
GROUP BY SUBSTRING(CAST(注文番号 AS VARCHAR),1,6)

SELECT 商品コード
FROM 注文
WHERE 商品コード LIKE 'Z%' 
GROUP BY 商品コード
HAVING SUM(数量) >= 100

UPDATE 注文
SET 商品コード = (SELECT 商品コード FROM 商品
WHERE 商品区分 = '2' AND 商品名 LIKE '%ブーツ%'
AND 商品名 LIKE '%雨%' AND 商品名 LIKE '%安心%')
WHERE 注文日='2024-03-15' 
AND 注文番号='202403150014' AND 注文枝番='1'

SELECT 商品コード,注文日 AS 売れた日付
FROM 注文
WHERE 商品コード IN(SELECT 商品コード FROM 商品 
WHERE 商品名 LIKE '%あったか%')
ORDER BY 注文日

SELECT 商品コード,SUM(数量) AS 商品合計
FROM 注文
GROUP BY 商品コード
HAVING  SUM(数量) > ALL(SELECT AVG(数量) FROM 注文 GROUP BY 商品コード) 

SELECT SUM(数量) AS 割引による販売数 ,
TRUNC(AVG(クーポン割引料),0) AS 平均割引額
FROM (SELECT * FROM 注文 
WHERE 商品コード = 'W0746' 
AND クーポン割引料 IS NOT NULL)


60 INSERT INTO 注文
VALUES('2024-03-21','202403210080',
(SELECT MAX(注文枝番)+1 FROM 注文
WHERE 注文番号 = '202403210080'),
'S1003','1',NULL);
INSERT INTO 注文
VALUES('2024-03-22','202403220901',
(SELECT MAX(注文枝番)+1 FROM 注文
WHERE 注文番号 = '202403220901'),
'A0052','2',500);

模範解答
INSERT INTO 注文
VALUES('2024-03-21','202403210080',
(SELECT MAX(注文枝番)+1 FROM 注文
WHERE 注文番号 = '202403210080' AND 注文日 = '2024-01-21'),
'S1003','1',NULL)
GROUP BY 注文日,注文番号;

SELECT C.注文番号,C.注文枝番,C.商品コード,S.商品名,C.数量
FROM 注文 AS C
JOIN 商品 AS S
ON C.商品コード = S.商品コード
WHERE C.注文番号 = '202401130115'
ORDER BY C.注文番号,C.注文枝番

SELECT C.注文日,C.注文番号,C.注文枝番,
C.数量,H.単価 * C.数量 AS 注文金額
FROM 注文 AS C
JOIN 廃番商品 AS H
ON C.商品コード = H.商品コード
WHERE C.商品コード = 'A0009' 
AND C.注文日 >= H.廃番日

SELECT S.商品コード,S.商品名,S.単価,
C.注文日,C.注文番号,C.数量, 
S.単価*C.数量 AS 売上金額
FROM 商品 AS S
JOIN 注文 AS C
ON S.商品コード = C.商品コード
WHERE S.商品コード ='S0604'
ORDER BY C.注文番号

SELECT C.商品コード,S.商品名
FROM 商品 AS S
JOIN 注文 AS C
ON S.商品コード = C.商品コード
WHERE C.注文日 >= '2022-08-01' 
AND C.注文日 < '2022-09-01'

SELECT C.商品コード,COALESCE(S.商品名,'廃番') AS 商品名
FROM 商品 AS S
RIGHT JOIN 注文 AS C
ON S.商品コード = C.商品コード
WHERE C.注文日 >= '2022-08-01' 
AND C.注文日 < '2022-09-01'

SELECT C.注文日,S.商品コード || ':' || S.商品名 AS 商品,
COALESCE(C.数量,0) AS 数量
FROM 商品 AS S
LEFT JOIN 注文 AS C
ON S.商品コード = C.商品コード
WHERE S.商品区分 ='3'

SELECT C.注文日,S.商品コード || ':'|| S.商品名 AS 商品,
COALESCE(C.数量,0) AS 数量
FROM 注文 AS C
RIGHT JOIN (SELECT 商品コード,商品名,商品区分 FROM 商品 
UNION 
SELECT 商品コード,'廃番済み' AS 商品名,商品区分 FROM 廃番商品) AS S
ON S.商品コード = C.商品コード
WHERE S.商品区分 ='3'

68,
自分の回答
SELECT C.注文日,C.注文番号,C.注文枝番,C.商品コード,
S.商品名,S.単価,C.数量,
(S.単価-COALESCE(クーポン割引料,0))*C.数量 
AS 注文金額
FROM (SELECT 商品コード,商品名,単価 FROM 商品
UNION
SELECT 商品コード,商品名,単価 FROM 廃番商品) AS S
JOIN 注文 AS C
ON S.商品コード =C.商品コード
WHERE C.注文番号 = '202304030010';

模範解答
SELECT C.注文日,C.注文番号,C.注文枝番,C.商品コード,
COALESCE(S.商品名,H.商品名),COALESCE(S.単価,H.単価),C.数量,
(COALESCE(S.単価,H.単価)-COALESCE(クーポン割引料,0))*C.数量 
AS 注文金額
FROM 注文 AS C
LEFT JOIN 商品 AS S
ON S.商品コード =C.商品コード
LEFT JOIN 廃番商品 AS H
ON C.商品コード =H.商品コード
WHERE C.注文番号 = '202304030010';


69-70 一旦放置

69
×　自分の回答（一旦ね）
SELECT S.商品コード,S.商品名,S.単価,
SUM(COALESCE(T.数量,0)) AS 売り上げた個数,
S.単価*SUM(COALESCE(T.数量,0)) AS 総売上金額
FROM 商品 AS S
LEFT JOIN 注文 AS T
ON S.商品コード = T.商品コード
WHERE SUBSTRING(S.商品コード,1,1) LIKE 'B%'
GROUP BY S.商品コード
ORDER BY S.商品コード

69模範
SELECT S.商品コード,S.商品名,S.単価,
COALESCE(T.数量, 0) AS 売上数量,
S.単価 * COALESCE(T.数量, 0) AS 総売上金額
FROM 商品 AS S
LEFT JOIN (SELECT 商品コード,SUM(数量) AS 数量
FROM 注文 WHERE 商品コード LIKE 'B%'
GROUP BY 商品コード) AS T
ON S.商品コード = T.商品コード
WHERE S.商品コード LIKE 'B%'
ORDER BY S.商品コード
ーーーーーーーーーーーーーーーーーー

SELECT id,名称,職業コード,hp,mp,状態コード
FROM パーティー

SELECT 名称 AS なまえ,hp AS 現在のHP,mp AS 現在のMP 
FROM パーティー

SELECT *
FROM イベント

SELECT イベント番号 AS 番号,イベント名称 AS 場面
FROM イベント

INSERT INTO パーティー
VALUES('A01','スガワラ','21',131,232,'03');
INSERT INTO パーティー
VALUES('A02','オーエ','10',156,84,'00');
INSERT INTO パーティー
VALUES('A03','イズミ','20',84,190,'00');

SELECT * FROM パーティー
WHERE id = 'C02'

UPDATE パーティー
SET hp = 120
WHERE id = 'A01'

SELECT id,名称,hp
FROM パーティー
WHERE hp < 100

SELECT id,名称,hp
FROM パーティー
WHERE hp < 100
 9番まで

SELECT イベント番号,イベント名称,タイプ FROM イベント
WHERE タイプ <> '3'

SELECT イベント番号,イベント名称 FROM イベント
WHERE イベント番号 <= 5

SELECT イベント番号,イベント名称 FROM イベント
WHERE イベント番号 >= 20

SELECT イベント番号,イベント名称 FROM イベント
WHERE 前提イベント番号 IS NULL

SELECT イベント番号,イベント名称,後続イベント番号 FROM イベント
WHERE 後続イベント番号 IS NOT NULL

UPDATE パーティー
SET 状態コード = '01'
WHERE 名称 LIKE '%ミ%'

SELECT id,名称,hp 
FROM パーティー
WHERE hp BETWEEN 120 AND 160

SELECT 名称,職業コード FROM パーティー
WHERE 職業コード IN('01','10','11')

SELECT 名称,状態コード FROM パーティー
WHERE 状態コード NOT IN('00','09')

SELECT * FROM パーティー
WHERE hp >= 100 AND mp >= 100

SELECT * FROM パーティー
WHERE id LIKE 'A%' AND 職業コード LIKE '2%'

SELECT * FROM イベント
WHERE タイプ = '1' 
AND 前提イベント番号 IS NOT NULL 
AND 後続イベント番号 IS NOT NULL

SELECT DISTINCT 状態コード
FROM パーティー

SELECT id,名称 FROM パーティー
ORDER BY id

SELECT 名称,hp,状態コード FROM パーティー
ORDER BY 状態コード,hp DESC

SELECT * FROM パーティー
ORDER BY hp DESC
OFFSET 0 ROWS
FETCH NEXT 3 ROWS ONLY

SELECT * FROM パーティー
ORDER BY mp DESC
OFFSET 2 ROWS
FETCH NEXT 3 ROWS ONLY

SELECT イベント番号 FROM イベント
EXCEPT
SELECT イベント番号 FROM 経験イベント
ORDER BY 1 

SELECT イベント番号 FROM イベント
WHERE タイプ = '2'
INTERSECT
SELECT イベント番号 FROM 経験イベント
WHERE クリア区分 = '1'

SELECT CASE
WHEN 職業コード LIKE '1%' THEN 'S'
WHEN 職業コード LIKE '2%' THEN 'M'
ELSE 'A'
END AS 職業区分,
職業コード,id,名称 FROM パーティー
ORDER BY 職業コード

SELECT 名称 AS 名前,
hp AS 現在のHP,hp + 50 AS 装備後のHP 
FROM パーティー
WHERE 職業コード IN('11','21')

UPDATE パーティー
SET mp = mp +20
WHERE id IN('A01','A03')

SELECT 名称 AS なまえ,
hp AS 現在のHP,
hp * 2 AS 予想されるダメージ
FROM パーティー
WHERE 職業コード = '11'

SELECT 名称 AS なまえ,hp || '/' || mp AS HPとMP,CASE 
WHEN 状態コード = '01'THEN '眠り'
WHEN 状態コード = '02'THEN '毒'
WHEN 状態コード = '03'THEN '沈黙'
WHEN 状態コード = '04'THEN '混乱'
WHEN 状態コード = '05'THEN '気絶'
WHEN 状態コード = '05'THEN NULL
END AS ステータス
FROM パーティー

37,△自分の回答
SELECT イベント番号,イベント名称,CASE
WHEN タイプ = '1' THEN '強制'
WHEN タイプ = '2' THEN 'フリー'
WHEN タイプ = '3' THEN '特殊'
END AS タイプ, 
CASE WHEN イベント番号 BETWEEN 1 AND 10 THEN '序盤'
WHEN イベント番号 BETWEEN 11 AND 17 THEN '中盤'
ELSE '終盤' END AS 発生時期
FROM イベント

37,模範解答
SELECT イベント番号,イベント名称,CASE
WHEN タイプ = '1' THEN '強制'
WHEN タイプ = '2' THEN 'フリー'
WHEN タイプ = '3' THEN '特殊'
END AS タイプ, 
CASE WHEN イベント番号 <= 10 THEN '序盤'
WHEN イベント番号 <= 17 THEN '中盤'
ELSE '終盤' END AS 発生時期
FROM イベント

SELECT 名称 AS なまえ,hp AS 現在のHP,
LENGTH(名称) * 10 AS 予想ダメージ
FROM パーティー

演算子を用いた場合
UPDATE パーティー
SET 状態コード = '04'
WHERE hp % 4 = 0  OR mp % 4 = 0
関数を用いた場合
UPDATE パーティー
SET 状態コード = '04'
WHERE MOD(hp,4) = 0  OR MOD(mp,4) = 0

SELECT TRUNC(777*0.7,0) AS 支払った金額 

UPDATE パーティー
SET hp = ROUND(hp * 1.3,0),
mp = ROUND(mp * 1.3 ,0)

SELECT 名称 AS なまえ,hp,
POWER(hp,0) AS 攻撃1回目,
POWER(hp,1) AS 攻撃2回目,
POWER(hp,2) AS 攻撃3回目
FROM パーティー
WHERE 職業コード = '10'

SELECT 名称 AS なまえ,hp,状態コード,CASE
WHEN hp <= 50 THEN 3 + CAST(状態コード AS INTEGER)
WHEN hp <= 100 THEN 2 + CAST(状態コード AS INTEGER)
WHEN hp <= 150 THEN 1 + CAST(状態コード AS INTEGER)
ELSE 0 + CAST(状態コード AS INTEGER) END AS リスク値
FROM パーティー
ORDER BY リスク値 DESC ,hp

SELECT COALESCE(CAST(前提イベント番号 AS VARCHAR),'前提なし') AS 前提イベント番号,
イベント番号,COALESCE(CAST(後続イベント番号 AS VARCHAR),'後続なし') AS 後続イベント番号
FROM イベント

SELECT MAX(hp)AS hpの最大値,MIN(hp)AS hpの最小値,AVG(hp)AS hpの平均値,
MAX(mp) AS mpの最大値,MIN(mp) AS mpの最小値,AVG(mp) AS mpの平均値
FROM パーティー

SELECT CASE
WHEN タイプ = '1' THEN '強制'
WHEN タイプ = '2' THEN 'フリー'
WHEN タイプ = '3' THEN '特殊'
END AS タイプ,COUNT(タイプ) AS イベントの数
FROM イベント
GROUP BY タイプ

SELECT クリア結果,COUNT(クリア結果)
FROM 経験イベント
WHERE クリア区分 = '1'
GROUP BY クリア結果
ORDER BY クリア結果

SELECT CASE 
WHEN SUM(mp) < 500  THEN '敵はみとれている'
WHEN SUM(mp) < 1000  THEN '敵は呆然としている'
WHEN SUM(mp) >= 1000  THEN '敵はひれ伏している'
END AS 小さな奇跡
FROM パーティー

SELECT CASE
WHEN クリア区分 = '1' THEN 'クリアした'
WHEN クリア区分 = '0' THEN '参加したがクリアしていない'
END AS 区分,COUNT(クリア区分) AS イベント数
FROM 経験イベント
GROUP BY クリア区分

SELECT SUBSTRING(CAST(職業コード AS VARCHAR),1,1) AS 職業タイプ,
MAX(hp)最大,MIN(hp)最小,AVG(hp)平均値,
MAX(mp)最大,MIN(mp)最小,AVG(mp)平均値
FROM パーティー
GROUP BY SUBSTRING(CAST(職業コード AS VARCHAR),1,1)

SELECT SUBSTRING(id,1,1) AS IDによる分類, 
AVG(hp) AS HPの平均,AVG(mp) AS MPの平均
FROM パーティー
GROUP BY SUBSTRING(id,1,1) 
HAVING AVG(hp) >= 100

SELECT SUM(CASE
WHEN hp < 100 THEN 1
WHEN hp >= 100 AND hp < 150 THEN 2
WHEN hp >= 150 AND hp < 200 THEN 3
WHEN hp >= 200 THEN 5 END )
AS 開けることのできる扉の合計数
FROM パーティー

 SELECT 名称 AS なまえ,hp AS 現在のHP,
ROUND(CAST(hp AS NUMERIC)/(SELECT SUM(hp) FROM パーティー)*100,1) 
||'%' AS パーティーでの割合
FROM パーティー
WHERE 職業コード = '01'

UPDATE パーティー
SET mp = mp + ROUND((SELECT SUM(mp)*0.1 
FROM パーティー WHERE 職業コード <> '20'),0)
WHERE 職業コード = '20'

55,模範解答
SELECT イベント番号,クリア結果
FROM 経験イベント
WHERE イベント番号 IN(SELECT イベント番号
FROM イベント 
WHERE タイプ IN('1','3')) AND クリア区分 = '1' 

55,自分の回答
SELECT イベント番号,クリア結果
FROM 経験イベント
WHERE イベント番号 IN(SELECT イベント番号
FROM イベント WHERE タイプ = '1' OR タイプ = '3') AND クリア区分 = '1' 

特に問題はないけど、タイプが複数ある場合はINを使った方がスッキリとして分かりやすいかも。

SELECT 名称 AS なまえ,mp
FROM パーティー
WHERE mp = (SELECT MAX(mp) FROM パーティー)

SELECT イベント番号,イベント名称
FROM イベント
WHERE イベント番号  NOT IN(SELECT イベント番号 FROM 経験イベント) 
ORDER BY イベント番号

58,自分の回答
SELECT COUNT(イベント番号)
FROM イベント
WHERE イベント番号 NOT IN(SELECT イベント番号 FROM 経験イベント) 

58,模範解答
SELECT COUNT(イベント番号)
FROM (SELECT イベント番号 FROM イベント 
EXCEPT SELECT イベント番号 FROM 経験イベント ) AS SUB

SELECT イベント番号,イベント名称
FROM イベント
WHERE イベント番号 < (SELECT イベント番号 FROM 経験イベント WHERE ルート番号 = 5)

SELECT イベント番号,イベント名称,前提イベント番号
FROM イベント
WHERE 前提イベント番号 = ANY(SELECT イベント番号 FROM 経験イベント WHERE クリア区分 = '1')

UPDATE 経験イベント
SET クリア区分 = '1',クリア結果 = 'B',ルート番号 = (SELECT MAX(ルート番号) + 1 FROM 経験イベント)
WHERE イベント番号 = 9 ;

61 
INSERT INTO 経験イベント
VALUES ((SELECT 後続イベント番号 FROM イベント WHERE イベント番号 = 9),0,NULL,NULL);

SELECT K.ルート番号,K.イベント番号,I.イベント名称,K.クリア結果
FROM 経験イベント AS K
JOIN イベント AS I
ON K.イベント番号 = I.イベント番号
WHERE K.クリア区分 = '1'
ORDER BY K.ルート番号

SELECT I.イベント番号,I.イベント名称,K.クリア区分 
FROM 経験イベント AS K
JOIN イベント AS I
ON K.イベント番号 = I.イベント番号
WHERE I.タイプ = '1'


SELECT I.イベント番号,I.イベント名称,COALESCE(K.クリア区分,'未クリア') AS クリア区分
FROM 経験イベント AS K
JOIN イベント AS I
ON K.イベント番号 = I.イベント番号
WHERE I.タイプ = '1'

65,
SELECT P.ID,P.名称 AS なまえ,
S.コード名称 AS 職業 , Z.コード名称 AS 状態
FROM パーティー AS P
JOIN (SELECT コード値,コード名称 FROM コード WHERE コード種別 = 1) AS S
ON P.職業コード = S.コード値
JOIN (SELECT コード値,コード名称 FROM コード WHERE コード種別 = 2) AS Z
ON P.状態コード = Z.コード値
ORDER BY ID

SELECT P.ID,COALESCE(P.名称,'仲間になっていない！') AS なまえ,S.コード名称 AS 職業 
FROM パーティー AS P
RIGHT JOIN (SELECT コード値,コード名称 FROM コード WHERE コード種別 = 1) AS S
ON P.職業コード = S.コード値

SELECT K.イベント番号,K.クリア区分,C.コード値 || ':' || C.コード名称 AS クリア結果
FROM 経験イベント AS K
FULL JOIN (SELECT コード値,コード名称 FROM コード WHERE コード種別 = 4) AS C
ON K.クリア結果 = C.コード値

68, まだ途中
SELECT I.イベント番号,I.イベント名称,I.前提イベント番号,SELECT(Z.イベント番号)
FROM イベント I
JOIN (SELECT イベント番号 FROM イベント WHERE 前提イベント IS NOT NULL) Z
ON I.イベント番号 = Z.イベント番号
WHERE I.前提イベント IS NOT NULL
（一回時間を置く）
