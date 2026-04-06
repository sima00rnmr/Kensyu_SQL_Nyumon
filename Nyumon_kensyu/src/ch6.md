SELECT SUM(年間降水量),AVG(最高気温),AVG(最低気温)
FROM 都市別気象観測

SELECT SUM(年間降水量),AVG(最高気温),AVG(最低気温)
FROM 都市別気象観測
WHERE 都市名 = '東京'

SELECT 都市名,AVG(降水量), MIN(最高気温),MAX(最低気温)
FROM 都市別気象観測
GROUP BY 都市名

SELECT 月,AVG(最高気温),AVG(最低気温)
FROM 都市別気象観測
GROUP BY 月

SELECT 都市名,MAX(最高気温)
FROM 都市別気象観測
GROUP BY 都市名
HAVING BY MAX(最高気温) >=38

SELECT 都市名,MIN(最高気温)
FROM 都市別気象観測
GROUP BY 都市名
HAVING BY MAX(最高気温) <=-10
------------------------------------

SELECT COUNT(*) AS 社員数
FROM 入退出管理
WHERE 退出 IS NULL // = NULLは使ってはだめ（値がない　に対して"="は使えない）

SELECT 社員名,COUNT(*) AS 入室回数 
FROM 入退出管理
WHERE 社員名
ORDER BY 2 DESC

SELECT CASE 事由区分 
WHEN '1' THEN'メンテナンス'
WHEN '2' THEN 'リリース作業'
WHEN '3' THEN '障害対応'
WHEN '9' THEN 'その他'
END AS 事由
COUNT(*) AS 入室回数
FROM 入退出管理
GROUP BY 事由区分

SELECT 社員名,COUNT(*) AS 入室回数 
FROM 入退出管理
GROUP BY 社員名
HAVING COUNT(*) >=10

SELECT COUNT(社員名) AS 対応人数 //対応した人数なのでCOUNTは行数ではなく社員の重複を削除
WHERE 事由区分 = '3'
FROM 入退出管理
GROUP BY 日付


