UPDATE 試験結果
SET 午後1 = 80*4 -(86+91+68)
WHIRE 受験者ID 'SW1046'

UPDATE 試験結果
SET 論述 = 68*4 -(65+53+70)
WHILE 受験者ID 'SW1350'

UPDATE 試験結果
SET 午前 = 56*4 -(59+56+36)
WHILE 受験者ID 'SW1877'

SELECT 合格者ID AS 合格者ID fROM 試験結果
WHIRE 午前 >= 60
AND 午後1 + 午後2 >= 120
AND (午前 + 午後1 + 午後2)*0.3 <= 論述

---------------------------------

UPDATE  回答者 
SET 国名 = CASE SUBSTRING (TRIM(メールアドレス),LENGTH(TRIM(メールアドレス))-1),2)
WHEN jp THEN '日本' 
WHEN uk THEN 'イギリス'
WHEN cn THEN '中国'
WHEN fr THEN 'フランス'
WHEN vn THEN 'ベトナム'

×　自分の回答（大幅に回答と異なるので取っておこう…）

SERECT CAST(TRUNC(年齢,1)+'代:'+ 
CASE 住居 WHEN C THEN '集合住宅'
WHEN D THEN '戸建て') AS 属性,メールアドレス 
FROM 回答者
WHIRE 年齢 <=20
AND 年齢 >=50
～～～模範～～～
SERECT TRIM(メールアドレス) AS メールアドレス,CASE 
WHEN 年齢 >= 20 AND 年齢 < 30 THEN '20代'
WHEN 年齢 >= 30 AND 年齢 < 40 THEN '30代'
WHEN 年齢 >= 40 AND 年齢 < 50 THEN '40代'
WHEN 年齢 >= 50 AND 年齢 < 60 THEN '50代' END
||':'||
CASE 住居 
WHEN C THEN '集合住宅' 
WHEN D THEN '戸建て'
END AS 属性 FROM 回答者

-------------------
×自分の回答
UPDATE 受注
SET 文字数= LENGTH(TRIM(文字)) //前後のスペースしか削除出来ないのでダメ
模範解答
UPDATE 受注
SET 文字数= LENGTH(REPLACE(文字,' ',''))


×自分のコード

SERECT 受注日,受注ID,文字数,書体名,単価,特別加工料
ORDER BY 受注日,受注ID
CASE 特別加工料 WHEN 文字数< 10 THEN '0'
WHEN 文字数 >= 10 THEN '500' END
FROM 受注
