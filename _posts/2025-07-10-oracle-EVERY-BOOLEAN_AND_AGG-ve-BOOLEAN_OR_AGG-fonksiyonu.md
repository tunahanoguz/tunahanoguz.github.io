---
title: "Oracle - EVERY, BOOLEAN_AND_AGG ve BOOLEAN_OR_AGG Fonksiyonu"
date: 2025-07-10 20:45:00 +0300
layout: post
categories: oracle
---

- `EVERY` ve `BOOLEAN_AND_AGG` fonksiyonu, belirtilen koşulun tüm satırlar için karşılandığı durumda `TRUE`, aksi durumda `FALSE` değerini döner.
- `BOOLEAN_OR_AGG` fonksiyonu, belirtilen koşulun en az bir satır için karşılandığı durumda `TRUE`, aksi durumda `FALSE` değerini döner.
- Üç fonksiyon da hem aggregate hem de analytic function olarak kullanılabilir.

| Syntax                                                                                               |
| ---------------------------------------------------------------------------------------------------- |
| `EVERY([DISTINCT\|ALL] boolean_expression) OVER ([partition_by_clause] [order_by_clause])`           |
| `BOOLEAN_AND_AGG([DISTINCT\|ALL] boolean_expression) OVER ([partition_by_clause] [order_by_clause])` |
| `BOOLEAN_OR_AGG([DISTINCT\|ALL] boolean_expression) OVER ([partition_by_clause] [order_by_clause])`  |

- `[DISTINCT|ALL]`
	- `DISTINCT`, fonksiyon içerisinde belirtilen kolon/ifadenin tüm satırlardan benzersiz olacak şekilde alınmasını sağlar.
	- `ALL`, fonksiyon içerisinde belirtilen kolon/ifadenin tüm satırlardan benzersiz olma amacı güdülmeden alınmasını sağlar. `ALL`, varsayılan davranıştır.
	- `[DISTINCT|ALL]` kullanımı, bu fonksiyon için anlamsızdır çünkü `boolean_expression`, yalnızca `TRUE` veya `FALSE` değerine sahiptir.
- `boolean_expression`, `BOOLEAN` tipinde bir kolon veya `BOOLEAN` tipinde bir değer oluşturacak bir SQL ifadesidir.
- `[partition_by_clause]`, fonksiyonun hangi gruplar üzerinde çalışacağını belirtir.
- `[order_by_clause]`, fonksiyonun satırlar üzerinde nasıl bir sıralamayla çalışacağını belirtir. Üç fonksiyon da belirtilen koşulun tüm satırlar üzerinde sağlanıp sağlanmadığını kontrol eder ve yalnızca `BOOLEAN` tipinde bir değer döner. Bu sebeple sıralamanın bir anlamı yoktur.

---

```sql
SELECT  EVERY(TUTAR > 999),
		EVERY(TUTAR > 1000),
		BOOLEAN_AND_AGG(TUTAR > 999),
		BOOLEAN_AND_AGG(TUTAR > 1000),
		BOOLEAN_OR_AGG(TUTAR > 999),
		BOOLEAN_OR_AGG(TUTAR > 1000)
FROM (
	SELECT 1000 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 2000 AS TUTAR FROM DUAL
);
```

| EVERY(TUTAR > 999) | EVERY(TUTAR > 1000) | BOOLEAN_AND_AGG(TUTAR > 999) | BOOLEAN_AND_AGG(TUTAR > 1000) | BOOLEAN_OR_AGG(TUTAR > 999) | BOOLEAN_OR_AGG(TUTAR > 1000) |
| ------------------ | ------------------- | ---------------------------- | ----------------------------- | --------------------------- | ---------------------------- |
| TRUE               | FALSE               | TRUE                         | FALSE                         | TRUE                        | TRUE                         |

---

Aşağıda örnek sorgularda kullanılan `SEHIRLER` tablosundaki kayıtlar yer almaktadır.

| ULKE    | BOLGE   | SEHIR     | NUFUS      |
| ------- | ------- | --------- | ---------- |
| Türkiye | Marmara | İstanbul  | 16.000.000 |
| Türkiye | Marmara | Bursa     | 3.100.000  |
| Türkiye | Ege     | İzmir     | 4.500.000  |
| Türkiye | Ege     | Aydın     | 1.200.000  |
| Almanya | Bavyera | Münih     | 1.500.000  |
| Almanya | Bavyera | Nürnberg  | 600.000    |
| Almanya | Hessen  | Frankfurt | 800.000    |
| Almanya | Hessen  | Kassel    | 200.000    |

<br>

```sql
SELECT  ULKE,
		BOLGE,
		SEHIR,
		NUFUS,
		EVERY(NUFUS > 199000) OVER (PARTITION BY ULKE),
		EVERY(NUFUS > 3099999) OVER (PARTITION BY ULKE),
		EVERY(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE),
		EVERY(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE)
FROM SEHIRLER
ORDER BY ULKE, BOLGE, SEHIR, NUFUS;
```

| ULKE    | BOLGE   | SEHIR     | NUFUS      | EVERY(NUFUS > 199000) OVER (PARTITION BY ULKE) | EVERY(NUFUS > 3099999) OVER (PARTITION BY ULKE) | EVERY(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE) | EVERY(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE) |
| ------- | ------- | --------- | ---------- | ---------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------ |
| Almanya | Bavyera | Münih     | 1.500.000  | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Almanya | Bavyera | Nürnberg  | 600.000    | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Almanya | Hessen  | Frankfurt | 800.000    | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Almanya | Hessen  | Kassel    | 200.000    | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Türkiye | Ege     | Aydın     | 1.200.000  | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Türkiye | Ege     | İzmir     | 4.500.000  | TRUE                                           | FALSE                                           | TRUE                                                  | FALSE                                                  |
| Türkiye | Marmara | Bursa     | 3.100.000  | TRUE                                           | FALSE                                           | TRUE                                                  | TRUE                                                   |
| Türkiye | Marmara | İstanbul  | 16.000.000 | TRUE                                           | FALSE                                           | TRUE                                                  | TRUE                                                   |

<br>

```sql
SELECT  ULKE,
		BOLGE,
		SEHIR,
		NUFUS,
		BOOLEAN_AND_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE),
		BOOLEAN_AND_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE),
		BOOLEAN_AND_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE),
		BOOLEAN_AND_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE)
FROM SEHIRLER
ORDER BY ULKE, BOLGE, SEHIR;
```

| ULKE    | BOLGE   | SEHIR     | NUFUS      | BOOLEAN_AND_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE) | BOOLEAN_AND_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE) | BOOLEAN_AND_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE) | BOOLEAN_AND_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE) |
| ------- | ------- | --------- | ---------- | -------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------------- | ---------------------------------------------------------------- |
| Almanya | Bavyera | Münih     | 1.500.000  | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Almanya | Bavyera | Nürnberg  | 600.000    | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Almanya | Hessen  | Frankfurt | 800.000    | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Almanya | Hessen  | Kassel    | 200.000    | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Türkiye | Ege     | Aydın     | 1.200.000  | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Türkiye | Ege     | İzmir     | 4.500.000  | TRUE                                                     | FALSE                                                     | TRUE                                                            | FALSE                                                            |
| Türkiye | Marmara | Bursa     | 3.100.000  | TRUE                                                     | FALSE                                                     | TRUE                                                            | TRUE                                                             |
| Türkiye | Marmara | İstanbul  | 16.000.000 | TRUE                                                     | FALSE                                                     | TRUE                                                            | TRUE                                                             |

<br>

```sql
SELECT  ULKE,
		BOLGE,
		SEHIR,
		NUFUS,
		BOOLEAN_OR_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE),
		BOOLEAN_OR_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE),
		BOOLEAN_OR_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE),
		BOOLEAN_OR_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE)
FROM SEHIRLER
ORDER BY ULKE, BOLGE, SEHIR;
```

| ULKE    | BOLGE   | SEHIR     | NUFUS      | BOOLEAN_OR_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE) | BOOLEAN_OR_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE) | BOOLEAN_OR_AGG(NUFUS > 199000) OVER (PARTITION BY ULKE, BOLGE) | BOOLEAN_OR_AGG(NUFUS > 3099999) OVER (PARTITION BY ULKE, BOLGE) |
| ------- | ------- | --------- | ---------- | ------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------- |
| Almanya | Bavyera | Münih     | 1.500.000  | TRUE                                                    | FALSE                                                    | TRUE                                                           | FALSE                                                           |
| Almanya | Bavyera | Nürnberg  | 600.000    | TRUE                                                    | FALSE                                                    | TRUE                                                           | FALSE                                                           |
| Almanya | Hessen  | Frankfurt | 800.000    | TRUE                                                    | FALSE                                                    | TRUE                                                           | FALSE                                                           |
| Almanya | Hessen  | Kassel    | 200.000    | TRUE                                                    | FALSE                                                    | TRUE                                                           | FALSE                                                           |
| Türkiye | Ege     | Aydın     | 1.200.000  | TRUE                                                    | TRUE                                                     | TRUE                                                           | TRUE                                                            |
| Türkiye | Ege     | İzmir     | 4.500.000  | TRUE                                                    | TRUE                                                     | TRUE                                                           | TRUE                                                            |
| Türkiye | Marmara | Bursa     | 3.100.000  | TRUE                                                    | TRUE                                                     | TRUE                                                           | TRUE                                                            |
| Türkiye | Marmara | İstanbul  | 16.000.000 | TRUE                                                    | TRUE                                                     | TRUE                                                           | TRUE                                                            |
