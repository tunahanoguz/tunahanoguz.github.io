---
title: "Oracle - NTILE Fonksiyonu"
date: 2025-06-24 20:30:00 +0300
layout: post
categories: oracle
---

- `NTILE` analitik fonksiyonu, sıralanmış bir veri setini belirtilen sayıda alt veri kümesine böler ve her satır için o satırın yer aldığı alt veri kümesi numarasını `NUMBER` tipinde döner.
- Alt veri kümesi numarası 1 ile başlar ve ardışık olarak devam eder.
- Alt veri kümelerinde yer alan kayıt sayıları arasındaki fark en fazla 1 olabilir. Eğer bölünecek alt veri kümesi sayısı için belirtilen değer kayıt sayısından fazla ise her satır için birer alt veri kümesi oluşturulur.
- Eğer veri seti belirtilen sayı kadar alt veri kümesine eşit olarak bölünemiyorsa, ilk alt veri kümesinden başlayarak alt veri kümelerinin bulundurabileceği kayıt sayıları arttırılır ve buna göre yerleşim yapılır. Bu yapılırken alt veri kümelerinde yer alan kayıt sayıları arasındaki farkın en fazla 1 olması kuralına dikkat edilir.

| Syntax                                                              |
| ------------------------------------------------------------------- |
| `NTILE(expression) OVER ([query_partition_clause] order_by_clause)` |

- `expression`, veri setinin bölüneceği alt veri kümesi sayısıdır. Pozitif bir tam sayı olmalıdır.
	- Pozitif olan ancak tam sayı olmayan bir sayı belirtildiğinde, sayı tam sayı olacak şekilde truncate edilir.
	- Negatif herhangi bir sayı verildiğinde, `ORA-01428: Argument expression is out of range.` hatası alınır.
	- Sayı olmayan bir değer belirtildiğinde ise, (örneğin; asd) aşağıdaki hata alınır.
		- `ORA-01722: unable to convert string value containing 'a' to a number: ORA-03302: (ORA-01722 details) invalid string value: asd`
- `query_partition_clause`, opsiyoneldir, veri setinin belirli gruplar içinde alt veri kümelerine ayrılmasını sağlar.
- `order_by_clause`, zorunludur ve veri setinin belirli bir sıralamaya göre alt veri kümelerine ayrılmasını sağlar.

<br>

```sql
SELECT  TUTAR,
    	NTILE(3) OVER(ORDER BY TUTAR)
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 60 AS TUTAR FROM DUAL
);
```

| TUTAR | NTILE |
| ----- | ----- |
| 10    | 1     |
| 20    | 1     |
| 30    | 2     |
| 40    | 2     |
| 50    | 3     |
| 60    | 3     |

<br>

```sql
SELECT  TUTAR,
    	NTILE(4) OVER(ORDER BY TUTAR)
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 60 AS TUTAR FROM DUAL
);
```

| TUTAR | NTILE |
| ----- | ----- |
| 10    | 1     |
| 20    | 1     |
| 30    | 2     |
| 40    | 2     |
| 50    | 3     |
| 60    | 4     |

<br>

```sql
SELECT  TUTAR,
	NTILE(7) OVER(ORDER BY TUTAR)
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 60 AS TUTAR FROM DUAL
);
```

| TUTAR | NTILE |
| ----- | ----- |
| 10    | 1     |
| 20    | 2     |
| 30    | 3     |
| 40    | 4     |
| 50    | 5     |
| 60    | 6     |

<br>

```sql
SELECT  TUTAR,
	NTILE(3.4) OVER(ORDER BY TUTAR)
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 60 AS TUTAR FROM DUAL
);
```

| TUTAR | NTILE |
| ----- | ----- |
| 10    | 1     |
| 20    | 1     |
| 30    | 2     |
| 40    | 2     |
| 50    | 3     |
| 60    | 3     |
