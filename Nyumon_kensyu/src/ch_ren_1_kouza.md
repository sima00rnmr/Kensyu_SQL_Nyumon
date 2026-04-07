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

SELECT * fROM 口座
WHERE (口座番号 LIKE'2______')
OR (名義 LIKE 'エ__　%コ')




