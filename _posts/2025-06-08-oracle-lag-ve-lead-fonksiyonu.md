---
title: "Oracle - LAG ve LEAD Fonksiyonu"
date: 2025-06-08 11:30:00 +0300
layout: post
categories: oracle
---

- `LAG` fonksiyonu, belirtilen sayı kadar önceki satırdan bir değeri elde etmeyi sağlar.
- `LEAD` fonksiyonu, belirtilen sayı kadar sonraki satırdan bir değeri elde etmeyi sağlar.

| Syntax                                                                                   |
| ---------------------------------------------------------------------------------------- |
| `LAG(expression [, offset [, default]]) OVER([query_partition_clause] order_by_clause)`  |
| `LEAD(expression [, offset [, default]]) OVER([query_partition_clause] order_by_clause)` |

- `expression`, bir kolondur veya değeri oluşturacak bir ifadedir.
- `offset`, kaç önceki/sonraki satıra bakılacağını ifade eden sayıdır. Varsayılan değeri 1'dir. (opsiyonel)
- `default`, bakılacak satır yoksa dönülecek varsayılan değerdir. Varsayılan değeri NULL'dur. (opsiyonel)
- `query_partition_clause`, değerin belli bir gruba göre elde edilmesini sağlar. Yalnızca grup içerisinde yer alan satırlara bakılır. (opsiyonel)
- `order_by_clause`, değerin hangi sıralama üzerinden elde edileceğini belirtir. (opsiyonel) Bu sıralama yalnızca analitik fonksiyon için geçerlidir, `SELECT` sorgusudan dönen kayıtların farklı bir sıralamada olma ihtimali vardır, `SELECT` sorgusunun sıralama davranışını değiştirmek için o sorgu için de açık bir şekilde `ORDER BY` kullanmak gerekir. `SELECT` sorgusu için yapılan sıralama, fonksiyonun çalışma şeklinde bir değişime sebep olmaz.

---

Aşağıda `LAG` ve `LEAD` fonksiyonu için kullanım örnekleri yer almaktadır.

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 1         | 10    | NULL           |
| 2         | 30    |     | 3         | 20    | 10             |
| 3         | 20    |     | 2         | 30    | 20             |
| 4         | 70    |     | 5         | 40    | 30             |
| 5         | 40    |     | 7         | 50    | 40             |
| 6         | 60    |     | 6         | 60    | 50             |
| 7         | 50    |     | 4         | 70    | 60             |
| 8         | NULL  |     | 8         | NULL  | 70             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 1         | 10    | NULL           |
| 2         | 30    |     | 3         | 20    | 10             |
| 3         | 20    |     | 2         | 30    | 20             |
| 4         | 70    |     | 5         | 40    | 30             |
| 5         | 40    |     | 7         | 50    | 40             |
| 6         | 60    |     | 6         | 60    | 50             |
| 7         | 50    |     | 4         | 70    | 60             |
| 8         | NULL  |     | 8         | NULL  | 70             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1, 100) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 1         | 10    | 100            |
| 2         | 30    |     | 3         | 20    | 10             |
| 3         | 20    |     | 2         | 30    | 20             |
| 4         | 70    |     | 5         | 40    | 30             |
| 5         | 40    |     | 7         | 50    | 40             |
| 6         | 60    |     | 6         | 60    | 50             |
| 7         | 50    |     | 4         | 70    | 60             |
| 8         | NULL  |     | 8         | NULL  | 70             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 1         | 10    | NULL           |
| 2         | 30    |     | 3         | 20    | NULL           |
| 3         | 20    |     | 2         | 30    | 10             |
| 4         | 70    |     | 5         | 40    | 20             |
| 5         | 40    |     | 7         | 50    | 30             |
| 6         | 60    |     | 6         | 60    | 40             |
| 7         | 50    |     | 4         | 70    | 50             |
| 8         | NULL  |     | 8         | NULL  | 60             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2, 100) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 1         | 10    | 100            |
| 2         | 30    |     | 3         | 20    | 100            |
| 3         | 20    |     | 2         | 30    | 10             |
| 4         | 70    |     | 5         | 40    | 20             |
| 5         | 40    |     | 7         | 50    | 30             |
| 6         | 60    |     | 6         | 60    | 40             |
| 7         | 50    |     | 4         | 70    | 50             |
| 8         | NULL  |     | 8         | NULL  | 60             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LEAD(TUTAR) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LEAD(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------- |
| 1         | 10    |     | 1         | 10    | 20              |
| 2         | 30    |     | 3         | 20    | 30              |
| 3         | 20    |     | 2         | 30    | 40              |
| 4         | 70    |     | 5         | 40    | 50              |
| 5         | 40    |     | 7         | 50    | 60              |
| 6         | 60    |     | 6         | 60    | 70              |
| 7         | 50    |     | 4         | 70    | NULL            |
| 8         | NULL  |     | 8         | NULL  | NULL            |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LEAD(TUTAR, 1) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LEAD(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------- |
| 1         | 10    |     | 1         | 10    | 20              |
| 2         | 30    |     | 3         | 20    | 30              |
| 3         | 20    |     | 2         | 30    | 40              |
| 4         | 70    |     | 5         | 40    | 50              |
| 5         | 40    |     | 7         | 50    | 60              |
| 6         | 60    |     | 6         | 60    | 70              |
| 7         | 50    |     | 4         | 70    | NULL            |
| 8         | NULL  |     | 8         | NULL  | NULL            |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LEAD(TUTAR, 1, 100) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LEAD(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------- |
| 1         | 10    |     | 1         | 10    | 20              |
| 2         | 30    |     | 3         | 20    | 30              |
| 3         | 20    |     | 2         | 30    | 40              |
| 4         | 70    |     | 5         | 40    | 50              |
| 5         | 40    |     | 7         | 50    | 60              |
| 6         | 60    |     | 6         | 60    | 70              |
| 7         | 50    |     | 4         | 70    | NULL            |
| 8         | NULL  |     | 8         | NULL  | 100             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LEAD(TUTAR, 2) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LEAD(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------- |
| 1         | 10    |     | 1         | 10    | 30              |
| 2         | 30    |     | 3         | 20    | 40              |
| 3         | 20    |     | 2         | 30    | 50              |
| 4         | 70    |     | 5         | 40    | 60              |
| 5         | 40    |     | 7         | 50    | 70              |
| 6         | 60    |     | 6         | 60    | NULL            |
| 7         | 50    |     | 4         | 70    | NULL            |
| 8         | NULL  |     | 8         | NULL  | NULL            |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LEAD(TUTAR, 2, 100) OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LEAD(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | --------------- |
| 1         | 10    |     | 1         | 10    | 30              |
| 2         | 30    |     | 3         | 20    | 40              |
| 3         | 20    |     | 2         | 30    | 50              |
| 4         | 70    |     | 5         | 40    | 60              |
| 5         | 40    |     | 7         | 50    | 70              |
| 6         | 60    |     | 6         | 60    | NULL            |
| 7         | 50    |     | 4         | 70    | 100             |
| 8         | NULL  |     | 8         | NULL  | 100             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 8         | NULL  | NULL           |
| 2         | 30    |     | 4         | 70    | NULL           |
| 3         | 20    |     | 6         | 60    | 70             |
| 4         | 70    |     | 7         | 50    | 60             |
| 5         | 40    |     | 5         | 40    | 50             |
| 6         | 60    |     | 2         | 30    | 40             |
| 7         | 50    |     | 3         | 20    | 30             |
| 8         | NULL  |     | 1         | 10    | 20             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 8         | NULL  | NULL           |
| 2         | 30    |     | 4         | 70    | NULL           |
| 3         | 20    |     | 6         | 60    | 70             |
| 4         | 70    |     | 7         | 50    | 60             |
| 5         | 40    |     | 5         | 40    | 50             |
| 6         | 60    |     | 2         | 30    | 40             |
| 7         | 50    |     | 3         | 20    | 30             |
| 8         | NULL  |     | 1         | 10    | 20             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1, 100) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 8         | NULL  | 100            |
| 2         | 30    |     | 4         | 70    | NULL           |
| 3         | 20    |     | 6         | 60    | 70             |
| 4         | 70    |     | 7         | 50    | 60             |
| 5         | 40    |     | 5         | 40    | 50             |
| 6         | 60    |     | 2         | 30    | 40             |
| 7         | 50    |     | 3         | 20    | 30             |
| 8         | NULL  |     | 1         | 10    | 20             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 8         | NULL  | NULL           |
| 2         | 30    |     | 4         | 70    | NULL           |
| 3         | 20    |     | 6         | 60    | NULL           |
| 4         | 70    |     | 7         | 50    | 70             |
| 5         | 40    |     | 5         | 40    | 60             |
| 6         | 60    |     | 2         | 30    | 50             |
| 7         | 50    |     | 3         | 20    | 40             |
| 8         | NULL  |     | 1         | 10    | 30             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2, 100) OVER(ORDER BY TUTAR DESC)
FROM SATISLAR
ORDER BY TUTAR DESC;
```

| MUSTERIID | TUTAR |     | MUSTERIID | TUTAR | LAG(TUTAR) ... |
| --------- | ----- | --- | --------- | ----- | -------------- |
| 1         | 10    |     | 8         | NULL  | 100            |
| 2         | 30    |     | 4         | 70    | 100            |
| 3         | 20    |     | 6         | 60    | NULL           |
| 4         | 70    |     | 7         | 50    | 70             |
| 5         | 40    |     | 5         | 40    | 60             |
| 6         | 60    |     | 2         | 30    | 50             |
| 7         | 50    |     | 3         | 20    | 40             |
| 8         | NULL  |     | 1         | 10    | 30             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAG(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | -------------- |
| Elektronik | 10    |     | Eğlence    | 70    | NULL           |
| Giyim      | 30    |     | Elektronik | 10    | NULL           |
| Gıda       | 20    |     | Elektronik | 60    | 10             |
| Eğlence    | 70    |     | Gıda       | 20    | NULL           |
| Sağlık     | 40    |     | Giyim      | 30    | NULL           |
| Elektronik | 60    |     | Giyim      | 50    | 30             |
| Giyim      | 50    |     | Sağlık     | 40    | NULL           |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 40             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAG(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | -------------- |
| Elektronik | 10    |     | Eğlence    | 70    | NULL           |
| Giyim      | 30    |     | Elektronik | 10    | NULL           |
| Gıda       | 20    |     | Elektronik | 60    | 10             |
| Eğlence    | 70    |     | Gıda       | 20    | NULL           |
| Sağlık     | 40    |     | Giyim      | 30    | NULL           |
| Elektronik | 60    |     | Giyim      | 50    | 30             |
| Giyim      | 50    |     | Sağlık     | 40    | NULL           |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 40             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 1, 100) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAG(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | -------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 100            |
| Giyim      | 30    |     | Elektronik | 10    | 100            |
| Gıda       | 20    |     | Elektronik | 60    | 10             |
| Eğlence    | 70    |     | Gıda       | 20    | 100            |
| Sağlık     | 40    |     | Giyim      | 30    | 100            |
| Elektronik | 60    |     | Giyim      | 50    | 30             |
| Giyim      | 50    |     | Sağlık     | 40    | 100            |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 40             |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAG(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | -------------- |
| Elektronik | 10    |     | Eğlence    | 70    | NULL           |
| Giyim      | 30    |     | Elektronik | 10    | NULL           |
| Gıda       | 20    |     | Elektronik | 60    | NULL           |
| Eğlence    | 70    |     | Gıda       | 20    | NULL           |
| Sağlık     | 40    |     | Giyim      | 30    | NULL           |
| Elektronik | 60    |     | Giyim      | 50    | NULL           |
| Giyim      | 50    |     | Sağlık     | 40    | NULL           |
| Sağlık     | NULL  |     | Sağlık     | NULL  | NULL           |

<br>

```sql
SELECT  MUSTERIID,
	TUTAR,
	LAG(TUTAR, 2, 100) OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| KATEGORI   | TUTAR |     | KATEGORI   | TUTAR | LAG(TUTAR) ... |
| ---------- | ----- | --- | ---------- | ----- | -------------- |
| Elektronik | 10    |     | Eğlence    | 70    | 100            |
| Giyim      | 30    |     | Elektronik | 10    | 100            |
| Gıda       | 20    |     | Elektronik | 60    | 100            |
| Eğlence    | 70    |     | Gıda       | 20    | 100            |
| Sağlık     | 40    |     | Giyim      | 30    | 100            |
| Elektronik | 60    |     | Giyim      | 50    | 100            |
| Giyim      | 50    |     | Sağlık     | 40    | 100            |
| Sağlık     | NULL  |     | Sağlık     | NULL  | 100            |
