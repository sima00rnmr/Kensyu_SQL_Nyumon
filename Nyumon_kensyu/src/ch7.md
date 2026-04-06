7_1-2は省略

×自分のコード
SELECT 飼育県,頭数(SELECT 飼育県,個体識別番号　FROM　個体識別) FROM 頭数集計

INSERT INTO 頭数集計
SELECT 飼育県,COUNT(個体識別)
ORDER BY 飼育県


残りは自宅で解く…