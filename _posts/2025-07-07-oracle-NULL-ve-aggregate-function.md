---
title: "Oracle - NULL ve Aggregate Function"
date: 2025-07-07 20:30:00 +0300
layout: post
categories: oracle
---

- `NULL`, birkaç istisna dışında, aggregate functionlar tarafından dikkate alınmaz. Fonksiyona `NULL` gönderen satırlar hiç yokmuş gibi davranılır.
- Özellikle `AVG` fonksiyonu için bu durum, fonksiyonun kullanım amacına göre sorun teşkil edebilir, bu sebeple dikkatli olunması gerekir. İlgili satırların dikkate alınması için, `NVL` gibi fonksiyonlarla `NULL` yerine geçecek default bir değer belirlenebilir.
- Yalnızca `COUNT` fonksiyonunun `COUNT(*)` ve `COUNT(sabit_deger)` kullanımları `NULL` gönderen satırları dikkate alır. Bunun sebebi, bu kullanımların amacının satır bazlı kayıt sayısını belirlemek olmasıdır.
	- `COUNT(kolon)` ve `COUNT(sql_expression)` kullanımları ise, `NULL` gönderen satırları dikkate almayacaktır. Bunun sebebi ise, bu tür kullanımların amacının, gerçek bir değer içeren/oluşturan kolon veya SQL ifadesinin yer aldığı satırların sayısını belirlemek olmasıdır.

```sql
SELECT  COUNT(TUTAR),
		    COUNT(NVL(TUTAR, 0)),
		    COUNT(*),
		    COUNT(1),
		    MAX(TUTAR),
		    MIN(TUTAR),
		    SUM(TUTAR),
		    AVG(TUTAR),
		    AVG(NVL(TUTAR, 0))
FROM (
	SELECT 1000 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 2000 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 3000 AS TUTAR FROM DUAL
	UNION ALL
	SELECT NULL AS TUTAR FROM DUAL
	UNION ALL
	SELECT 4000 AS TUTAR FROM DUAL
);
```

| COUNT(TUTAR) | COUNT(NVL(TUTAR, 0)) | COUNT(*) | COUNT(1) | MAX(TUTAR) | MIN(TUTAR) | SUM(TUTAR) | AVG(TUTAR) | AVG(NVL(TUTAR, 0)) |
| ------------ | -------------------- | -------- | -------- | ---------- | ---------- | ---------- | ---------- | ------------------ |
| 4            | 5                    | 5        | 5        | 4000       | 1000       | 10000      | 2500       | 2000               |
