---
title: "Oracle - FIRST_VALUE, LAST_VALUE ve NTH_VALUE Fonksiyonu"
date: 2025-06-12 12:30:00 +0300
layout: post
categories: oracle
---

## FIRST_VALUE Fonksiyonu

`FIRST_VALUE` fonksiyonu, bir dizi değerden belli bir sıralamaya göre ilk değeri getiren bir analitik fonksiyondur.

| Syntax                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------ |
| `FIRST_VALUE(expression) [RESPECT NULLS \| IGNORE NULLS] OVER ([query_partition_clause] [order_by_clause [windowing_clause])`  |
| `FIRST_VALUE(expression [RESPECT NULLS \| IGNORE NULLS]) OVER ([query_partition_clause] [order_by_clause [windowing_clause]])` |

- `expression`, bir kolondur veya değeri oluşturacak bir ifadedir.
- `[RESPECT NULLS | IGNORE NULLS]`, `NULL` değerlerin analitik fonksiyon tarafından dikkate alınıp alınmayacağını belirler. Eğer belirtilmezse varsayılan değeri `RESPECT NULLS` olur. `IGNORE NULLS` olarak belirtilse bile tüm değerler `NULL` ise fonksiyonun dönüş değeri `NULL` olur. (opsiyonel)
- `[PARTITION CLAUSE]`, değerin belli bir gruba göre elde edilmesini sağlar. (opsiyonel)
- `[ORDER BY CLAUSE]`, değerin hangi sıralama üzerinden elde edileceğini belirtir. Bu sıralama yalnızca analitik fonksiyon için geçerlidir, `SELECT` sorgusudan dönen kayıtların farklı bir sıralamada olma ihtimali vardır, `SELECT` sorgusunun sıralama davranışını değiştirmek için o sorgu için de açık bir şekilde `ORDER BY` kullanmak gerekir. `SELECT` sorgusu için yapılan sıralama, fonksiyonun çalışma şeklinde bir değişime sebep olmaz. (opsiyonel)
- `[WINDOWING CLAUSE]` için detaylı açıklamalara [buradan](oracle-windowing-clause "Oracle - Windowing Clause") ulaşılabilir. (opsiyonel)

Aşağıda `FIRST_VALUE` fonksiyonunun kullanım örnekleri yer almaktadır. `WINDOWING CLAUSE` için varsayılan değerin `UNBOUNDED PRECEDING AND CURRENT ROW` olduğu unutulmamalıdır.

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 1         | 10    | 10                     |
| 2         | 30    |     | 3         | 20    | 10                     |
| 3         | 20    |     | 2         | 30    | 10                     |
| 4         | 70    |     | 5         | 40    | 10                     |
| 5         | 40    |     | 7         | 50    | 10                     |
| 6         | 60    |     | 6         | 60    | 10                     |
| 7         | 50    |     | 4         | 70    | 10                     |
| 8         | NULL  |     | 8         | NULL  | 10                     |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                   |
| 2         | 30    |     | 4         | 70    | NULL                   |
| 3         | 20    |     | 6         | 60    | NULL                   |
| 4         | 70    |     | 7         | 50    | NULL                   |
| 5         | 40    |     | 5         | 40    | NULL                   |
| 6         | 60    |     | 2         | 30    | NULL                   |
| 7         | 50    |     | 3         | 20    | NULL                   |
| 8         | NULL  |     | 1         | 10    | NULL                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR) RESPECT NULLS OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                   |
| 2         | 30    |     | 4         | 70    | NULL                   |
| 3         | 20    |     | 6         | 60    | NULL                   |
| 4         | 70    |     | 7         | 50    | NULL                   |
| 5         | 40    |     | 5         | 40    | NULL                   |
| 6         | 60    |     | 2         | 30    | NULL                   |
| 7         | 50    |     | 3         | 20    | NULL                   |
| 8         | NULL  |     | 1         | 10    | NULL                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR RESPECT NULLS) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                   |
| 2         | 30    |     | 4         | 70    | NULL                   |
| 3         | 20    |     | 6         | 60    | NULL                   |
| 4         | 70    |     | 7         | 50    | NULL                   |
| 5         | 40    |     | 5         | 40    | NULL                   |
| 6         | 60    |     | 2         | 30    | NULL                   |
| 7         | 50    |     | 3         | 20    | NULL                   |
| 8         | NULL  |     | 1         | 10    | NULL                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR) IGNORE NULLS OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                   |
| 2         | 30    |     | 4         | 70    | 70                     |
| 3         | 20    |     | 6         | 60    | 70                     |
| 4         | 70    |     | 7         | 50    | 70                     |
| 5         | 40    |     | 5         | 40    | 70                     |
| 6         | 60    |     | 2         | 30    | 70                     |
| 7         | 50    |     | 3         | 20    | 70                     |
| 8         | NULL  |     | 1         | 10    | 70                     |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    FIRST_VALUE(TUTAR IGNORE NULLS) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | FIRST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | ---------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                   |
| 2         | 30    |     | 4         | 70    | 70                     |
| 3         | 20    |     | 6         | 60    | 70                     |
| 4         | 70    |     | 7         | 50    | 70                     |
| 5         | 40    |     | 5         | 40    | 70                     |
| 6         | 60    |     | 2         | 30    | 70                     |
| 7         | 50    |     | 3         | 20    | 70                     |
| 8         | NULL  |     | 1         | 10    | 70                     |

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    FIRST_VALUE(TUTAR) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | FIRST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | ---------------------- |
| Elektronik | 10    |     | Gıda       | 20    | 20                     |
| Giyim      | 30    |     | Giyim      | 30    | 30                     |
| Gıda       | 20    |     | Giyim      | 50    | 30                     |
| Eğlence    | 70    |     | Sağlık     | 40    | 40                     |
| Sağlık     | 40    |     | Sağlık     | NULL  | 40                     |
| Elektronik | 60    |     | Eğlence    | 70    | 70                     |
| Giyim      | 50    |     | Elektronik | 10    | 10                     |
| Sağlık     | NULL  |     | Elektronik | 60    | 10                     |

Sonuçtan görüleceği üzere, kategori bazlı bir sıralama yapılmadı. Her ne kadar tutarlar kategori bazlı sıralı gelmiş olsa da bu sıralama da garanti olmadığı için `SELECT` sorgusunda açık bir şekilde `ORDER BY` kullanılmalıdır.

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    FIRST_VALUE(TUTAR) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | FIRST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | ---------------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 70                     |
| Giyim      | 30    |     | Elektronik | 10    | 10                     |
| Gıda       | 20    |     | Elektronik | 60    | 10                     |
| Eğlence    | 70    |     | Gıda       | 20    | 20                     |
| Sağlık     | 40    |     | Giyim      | 30    | 30                     |
| Elektronik | 60    |     | Giyim      | 50    | 30                     |
| Giyim      | 50    |     | Sağlık     | 40    | 40                     |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 40                     |

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    FIRST_VALUE(TUTAR) OVER(PARTITION BY KATEGORI ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY KATEGORI ASC, TUTAR DESC;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | FIRST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | ---------------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 70                     |
| Giyim      | 30    |     | Elektronik | 60    | 60                     |
| Gıda       | 20    |     | Elektronik | 10    | 60                     |
| Eğlence    | 70    |     | Gıda       | 20    | 20                     |
| Sağlık     | 40    |     | Giyim      | 50    | 50                     |
| Elektronik | 60    |     | Giyim      | 30    | 50                     |
| Giyim      | 50    |     | Sağlık     | NULL  | NULL                   |
| Sağlık     | NULL  |     | Sağlık     | 40    | NULL                   |

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    FIRST_VALUE(TUTAR) IGNORE NULLS OVER(PARTITION BY KATEGORI ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY KATEGORI ASC, TUTAR DESC;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | FIRST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | ---------------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 70                     |
| Giyim      | 30    |     | Elektronik | 60    | 60                     |
| Gıda       | 20    |     | Elektronik | 10    | 60                     |
| Eğlence    | 70    |     | Gıda       | 20    | 20                     |
| Sağlık     | 40    |     | Giyim      | 50    | 50                     |
| Elektronik | 60    |     | Giyim      | 30    | 50                     |
| Giyim      | 50    |     | Sağlık     | NULL  | NULL                   |
| Sağlık     | NULL  |     | Sağlık     | 40    | 40                     |

---

## LAST_VALUE Fonksiyonu

`LAST_VALUE` fonksiyonu, bir dizi değerden belli bir sıralamaya göre son değeri getiren bir analitik fonksiyondur.

| Syntax                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------- |
| `LAST_VALUE(expression) [RESPECT NULLS \| IGNORE NULLS] OVER ([query_partition_clause] [order_by_clause [windowing_clause])`  |
| `LAST_VALUE(expression [RESPECT NULLS \| IGNORE NULLS]) OVER ([query_partition_clause] [order_by_clause [windowing_clause]])` |

- `expression`, bir kolondur veya değeri oluşturacak bir ifadedir.
- `[RESPECT NULLS | IGNORE NULLS]`, `NULL` değerlerin analitik fonksiyon tarafından dikkate alınıp alınmayacağını belirler. Eğer belirtilmezse varsayılan değeri `RESPECT NULLS` olur. `IGNORE NULLS` olarak belirtilse bile tüm değerler `NULL` ise fonksiyonun dönüş değeri `NULL` olur. (opsiyonel)
- `[PARTITION CLAUSE]`, değerin belli bir gruba göre elde edilmesini sağlar. (opsiyonel)
- `[ORDER BY CLAUSE]`, değerin hangi sıralama üzerinden elde edileceğini belirtir. Bu sıralama yalnızca analitik fonksiyon için geçerlidir, `SELECT` sorgusudan dönen kayıtların farklı bir sıralamada olma ihtimali vardır, `SELECT` sorgusunun sıralama davranışını değiştirmek için o sorgu içinde açık bir şekilde `ORDER BY` kullanmak gerekir. `SELECT` sorgusu için yapılan sıralama, fonksiyonun çalışma şeklinde bir değişime sebep olmaz. (opsiyonel)
- `[WINDOWING CLAUSE]` için detaylı açıklamalara buradan ulaşılabilir. (opsiyonel)

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    LAST_VALUE(TUTAR) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------------- |
| 1         | 10    |     | 1         | 10    | 10                    |
| 2         | 30    |     | 3         | 20    | 20                    |
| 3         | 20    |     | 2         | 30    | 30                    |
| 4         | 70    |     | 5         | 40    | 40                    |
| 5         | 40    |     | 7         | 50    | 50                    |
| 6         | 60    |     | 6         | 60    | 60                    |
| 7         | 50    |     | 4         | 70    | 70                    |
| 8         | NULL  |     | 8         | NULL  | NULL                  |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    LAST_VALUE(TUTAR) IGNORE NULLS OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------------- |
| 1         | 10    |     | 1         | 10    | 10                    |
| 2         | 30    |     | 3         | 20    | 20                    |
| 3         | 20    |     | 2         | 30    | 30                    |
| 4         | 70    |     | 5         | 40    | 40                    |
| 5         | 40    |     | 7         | 50    | 50                    |
| 6         | 60    |     | 6         | 60    | 60                    |
| 7         | 50    |     | 4         | 70    | 70                    |
| 8         | NULL  |     | 8         | NULL  | 70                    |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    LAST_VALUE(TUTAR) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                  |
| 2         | 30    |     | 4         | 70    | 70                    |
| 3         | 20    |     | 6         | 60    | 60                    |
| 4         | 70    |     | 7         | 50    | 50                    |
| 5         | 40    |     | 5         | 40    | 40                    |
| 6         | 60    |     | 2         | 30    | 30                    |
| 7         | 50    |     | 3         | 20    | 20                    |
| 8         | NULL  |     | 1         | 10    | 10                    |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    LAST_VALUE(TUTAR) IGNORE NULLS OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAST_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------------- |
| 1         | 10    |     | 8         | NULL  | NULL                  |
| 2         | 30    |     | 4         | 70    | 70                    |
| 3         | 20    |     | 6         | 60    | 60                    |
| 4         | 70    |     | 7         | 50    | 50                    |
| 5         | 40    |     | 5         | 40    | 40                    |
| 6         | 60    |     | 2         | 30    | 30                    |
| 7         | 50    |     | 3         | 20    | 20                    |
| 8         | NULL  |     | 1         | 10    | 10                    |

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    LAST_VALUE(TUTAR) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | --------------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 70                    |
| Giyim      | 30    |     | Elektronik | 10    | 10                    |
| Gıda       | 20    |     | Elektronik | 60    | 60                    |
| Eğlence    | 70    |     | Gıda       | 20    | 20                    |
| Sağlık     | 40    |     | Giyim      | 30    | 30                    |
| Elektronik | 60    |     | Giyim      | 50    | 50                    |
| Giyim      | 50    |     | Sağlık     | 40    | 40                    |
| Sağlık     | NULL  |     | Sağlık     | NULL  | NULL                  |

<br>

```sql
SELECT  KATEGORI,
		    TUTAR,
		    LAST_VALUE(TUTAR) IGNORE NULLS OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAST_VALUE(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | --------------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 70                    |
| Giyim      | 30    |     | Elektronik | 10    | 10                    |
| Gıda       | 20    |     | Elektronik | 60    | 60                    |
| Eğlence    | 70    |     | Gıda       | 20    | 20                    |
| Sağlık     | 40    |     | Giyim      | 30    | 30                    |
| Elektronik | 60    |     | Giyim      | 50    | 50                    |
| Giyim      | 50    |     | Sağlık     | 40    | 40                    |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 40                    |

---

## NTH_VALUE Fonksiyonu

`NTH_VALUE` fonksiyonu, bir dizi değerden belli bir sıralamaya göre n'inci değeri getiren bir analitik fonksiyondur.

| Syntax                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NTH_VALUE(expression, n) [FROM FIRST \| FROM LAST] [RESPECT NULLS \| IGNORE NULLS] OVER ([query_partition_clause] [order_by_clause [windowing_clause])` |

- `expression`, bir kolondur veya değeri oluşturacak bir ifadedir.
- `n`, kaçıncı değerin analitik fonksiyon tarafından dönüleceğini belirtir.
- `[RESPECT NULLS | IGNORE NULLS]`, `NULL` değerlerin analitik fonksiyon tarafından dikkate alınıp alınmayacağını belirler. Eğer belirtilmezse varsayılan değeri `RESPECT NULLS` olur. `IGNORE NULLS` olarak belirtilse bile tüm değerler `NULL` ise fonksiyonun dönüş değeri `NULL` olur. (opsiyonel)
- `[PARTITION CLAUSE]`, değerin belli bir gruba göre elde edilmesini sağlar. (opsiyonel)
- `[ORDER BY CLAUSE]`, değerin hangi sıralama üzerinden elde edileceğini belirtir. Bu sıralama yalnızca analitik fonksiyon için geçerlidir, `SELECT` sorgusudan dönen kayıtların farklı bir sıralamada olma ihtimali vardır, `SELECT` sorgusunun sıralama davranışını değiştirmek için o sorgu içinde açık bir şekilde `ORDER BY` kullanmak gerekir. `SELECT` sorgusu için yapılan sıralama, fonksiyonun çalışma şeklinde bir değişime sebep olmaz. (opsiyonel)
- `[WINDOWING CLAUSE]` için detaylı açıklamalara buradan ulaşılabilir. (opsiyonel)
- `[FROM FIRST | FROM LAST]`, n'inci değerin analitik fonksiyon özelindeki sıralamada baştan mı yoksa sondan mı alınacağını belirtir. `FROM FIRST` varsayılan değeridir. (opsiyonel)

Aşağıda `NTH_VALUE` fonksiyonu için örnekler yer almaktadır. `WINDOWING CLAUSE` için varsayılan değerin `UNBOUNDED PRECEDING AND CURRENT ROW` olduğu unutulmamalıdır.

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) FROM FIRST OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 10                   |
| 2         | 30    |     | 3         | 20    | 10                   |
| 3         | 20    |     | 2         | 30    | 10                   |
| 4         | 70    |     | 5         | 40    | 10                   |
| 5         | 40    |     | 7         | 50    | 10                   |
| 6         | 60    |     | 6         | 60    | 10                   |
| 7         | 50    |     | 4         | 70    | 10                   |
| 8         | NULL  |     | 8         | NULL  | 10                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) FROM FIRST OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | NULL                 |
| 2         | 30    |     | 3         | 20    | 20                   |
| 3         | 20    |     | 2         | 30    | 20                   |
| 4         | 70    |     | 5         | 40    | 20                   |
| 5         | 40    |     | 7         | 50    | 20                   |
| 6         | 60    |     | 6         | 60    | 20                   |
| 7         | 50    |     | 4         | 70    | 20                   |
| 8         | NULL  |     | 8         | NULL  | 20                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) FROM LAST OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 10                   |
| 2         | 30    |     | 3         | 20    | 20                   |
| 3         | 20    |     | 2         | 30    | 30                   |
| 4         | 70    |     | 5         | 40    | 40                   |
| 5         | 40    |     | 7         | 50    | 50                   |
| 6         | 60    |     | 6         | 60    | 60                   |
| 7         | 50    |     | 4         | 70    | 70                   |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) FROM LAST IGNORE NULLS OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 10                   |
| 2         | 30    |     | 3         | 20    | 20                   |
| 3         | 20    |     | 2         | 30    | 30                   |
| 4         | 70    |     | 5         | 40    | 40                   |
| 5         | 40    |     | 7         | 50    | 50                   |
| 6         | 60    |     | 6         | 60    | 60                   |
| 7         | 50    |     | 4         | 70    | 70                   |
| 8         | NULL  |     | 8         | NULL  | 70                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) FROM LAST OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | NULL                 |
| 2         | 30    |     | 3         | 20    | 10                   |
| 3         | 20    |     | 2         | 30    | 20                   |
| 4         | 70    |     | 5         | 40    | 30                   |
| 5         | 40    |     | 7         | 50    | 40                   |
| 6         | 60    |     | 6         | 60    | 50                   |
| 7         | 50    |     | 4         | 70    | 60                   |
| 8         | NULL  |     | 8         | NULL  | 70                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) FROM LAST IGNORE NULLS OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | NULL                 |
| 2         | 30    |     | 3         | 20    | 10                   |
| 3         | 20    |     | 2         | 30    | 20                   |
| 4         | 70    |     | 5         | 40    | 30                   |
| 5         | 40    |     | 7         | 50    | 40                   |
| 6         | 60    |     | 6         | 60    | 50                   |
| 7         | 50    |     | 4         | 70    | 60                   |
| 8         | NULL  |     | 8         | NULL  | 60                   |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 10                   |
| 2         | 30    |     | 3         | 20    | 20                   |
| 3         | 20    |     | 2         | 30    | 30                   |
| 4         | 70    |     | 5         | 40    | 40                   |
| 5         | 40    |     | 7         | 50    | 50                   |
| 6         | 60    |     | 6         | 60    | 60                   |
| 7         | 50    |     | 4         | 70    | 70                   |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) IGNORE NULLS OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 10                   |
| 2         | 30    |     | 3         | 20    | 20                   |
| 3         | 20    |     | 2         | 30    | 30                   |
| 4         | 70    |     | 5         | 40    | 40                   |
| 5         | 40    |     | 7         | 50    | 50                   |
| 6         | 60    |     | 6         | 60    | 60                   |
| 7         | 50    |     | 4         | 70    | 70                   |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 20                   |
| 2         | 30    |     | 3         | 20    | 30                   |
| 3         | 20    |     | 2         | 30    | 40                   |
| 4         | 70    |     | 5         | 40    | 50                   |
| 5         | 40    |     | 7         | 50    | 60                   |
| 6         | 60    |     | 6         | 60    | 70                   |
| 7         | 50    |     | 4         | 70    | NULL                 |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 2) IGNORE NULLS OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 20                   |
| 2         | 30    |     | 3         | 20    | 30                   |
| 3         | 20    |     | 2         | 30    | 40                   |
| 4         | 70    |     | 5         | 40    | 50                   |
| 5         | 40    |     | 7         | 50    | 60                   |
| 6         | 60    |     | 6         | 60    | 70                   |
| 7         | 50    |     | 4         | 70    | NULL                 |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) FROM LAST OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | NULL                 |
| 2         | 30    |     | 3         | 20    | NULL                 |
| 3         | 20    |     | 2         | 30    | NULL                 |
| 4         | 70    |     | 5         | 40    | NULL                 |
| 5         | 40    |     | 7         | 50    | NULL                 |
| 6         | 60    |     | 6         | 60    | NULL                 |
| 7         | 50    |     | 4         | 70    | NULL                 |
| 8         | NULL  |     | 8         | NULL  | NULL                 |

<br>

```sql
SELECT  MUSTERIID,
		    TUTAR,
		    NTH_VALUE(TUTAR, 1) FROM LAST IGNORE NULLS OVER(ORDER BY TUTAR RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | NTH_VALUE(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------------- |
| 1         | 10    |     | 1         | 10    | 70                   |
| 2         | 30    |     | 3         | 20    | 70                   |
| 3         | 20    |     | 2         | 30    | 70                   |
| 4         | 70    |     | 5         | 40    | 70                   |
| 5         | 40    |     | 7         | 50    | 70                   |
| 6         | 60    |     | 6         | 60    | 70                   |
| 7         | 50    |     | 4         | 70    | 70                   |
| 8         | NULL  |     | 8         | NULL  | 70                   |
