---
title: "Oracle - ANY_VALUE Fonksiyonu"
date: 2025-07-05 20:00:00 +0300
layout: post
categories: oracle
---

`ANY_VALUE` fonksiyonu, `GROUP BY` içeren bir sorguda, `GROUP BY` içerisinde yer almayan bir kolon veya SQL ifadesinin herhangi bir değerinin elde edilmesini sağlayan bir fonksiyondur. Elde edilen değer, Oracle veritabanının her grup için verileri çektiği sıralama üzerinden birinci satırdan alınır. Bu sıralama `ORDER BY` clause üzerinden belirlenmez, Oracle veritabanının verileri çektiği sıralama esastır. Bu sıralamanın belirlenmesi için birçok faktör vardır ve sorgu her çalıştırıldığında verilerin çekilme sırası değişebilir. Bu sebeple `ANY_VALUE` fonksiyonu ile elde edilecek değerler deterministik değildir.

| Syntax                  |
| ----------------------- |
| `ANY_VALUE(expression)` |

---

Aşağıda örnek sorgularda kullanılan `CALISANLAR` tablosundaki kayıtlar yer almaktadır.

| CALISAN_ID | AD       | SOYAD      | MAAS | DEPARTMAN      | ROL       |
| ---------- | -------- | ---------- | ---- | -------------- | --------- |
| 2          | John     | Doe        | 1000 | Raporlama      | Yazılımcı |
| 1          | Victoria | Jones      | 2000 | Mobil Uygulama | Yazılımcı |
| 3          | Harper   | White      | 3000 | Raporlama      | Yazılımcı |
| 5          | Hannah   | Edwards    | 4000 | Mobil Uygulama | Yazılımcı |
| 4          | Luna     | Howard     | 5000 | Mobil Uygulama | Analist   |
| 7          | Liliana  | Richardson | 6000 | Raporlama      | Analist   |
| 6          | Riley    | Chavez     | 7000 | Mobil Uygulama | Analist   |
| 8          | Maria    | Evans      | 8000 | Raporlama      | Analist   |

<br>

```sql
SELECT DEPARTMAN, ROL, ANY_VALUE(AD), ANY_VALUE(SOYAD), AVG(MAAS)
FROM CALISANLAR
GROUP BY DEPARTMAN, ROL
ORDER BY DEPARTMAN, ROL;
```

| DEPARTMAN      | ROL       | ANY_VALUE(AD) | ANY_VALUE(SOYAD) | AVG(MAAS) |
| -------------- | --------- | ------------- | ---------------- | --------- |
| Mobil Uygulama | Analist   | Luna          | Howard           | 6000      |
| Mobil Uygulama | Yazılımcı | Victoria      | Jones            | 3000      |
| Raporlama      | Analist   | Liliana       | Richardson       | 7000      |
| Raporlama      | Yazılımcı | John          | Doe              | 2000      |

<br>

```sql
SELECT DEPARTMAN, ROL, ANY_VALUE(AD), ANY_VALUE(SOYAD), AVG(MAAS)
FROM CALISANLAR
GROUP BY DEPARTMAN, ROL
ORDER BY DEPARTMAN, ROL DESC;
```

| DEPARTMAN      | ROL       | ANY_VALUE(AD) | ANY_VALUE(SOYAD) | AVG(MAAS) |
| -------------- | --------- | ------------- | ---------------- | --------- |
| Mobil Uygulama | Yazılımcı | Victoria      | Jones            | 3000      |
| Mobil Uygulama | Analist   | Luna          | Howard           | 6000      |
| Raporlama      | Yazılımcı | John          | Doe              | 2000      |
| Raporlama      | Analist   | Liliana       | Richardson       | 7000      |

<br>

```sql
SELECT DEPARTMAN, ROL, ANY_VALUE(AD), ANY_VALUE(SOYAD), AVG(MAAS)
FROM CALISANLAR
GROUP BY DEPARTMAN, ROL
ORDER BY DEPARTMAN DESC, ROL;
```

| DEPARTMAN      | ROL       | ANY_VALUE(AD) | ANY_VALUE(SOYAD) | AVG(MAAS) |
| -------------- | --------- | ------------- | ---------------- | --------- |
| Raporlama      | Analist   | Liliana       | Richardson       | 7000      |
| Raporlama      | Yazılımcı | John          | Doe              | 2000      |
| Mobil Uygulama | Analist   | Luna          | Howard           | 6000      |
| Mobil Uygulama | Yazılımcı | Victoria      | Jones            | 3000      |

<br>

```sql
SELECT DEPARTMAN, ROL, ANY_VALUE(AD), ANY_VALUE(SOYAD), AVG(MAAS)
FROM CALISANLAR
GROUP BY DEPARTMAN, ROL
ORDER BY DEPARTMAN DESC, ROL DESC;
```

| DEPARTMAN      | ROL       | ANY_VALUE(AD) | ANY_VALUE(SOYAD) | AVG(MAAS) |
| -------------- | --------- | ------------- | ---------------- | --------- |
| Raporlama      | Yazılımcı | John          | Doe              | 2000      |
| Raporlama      | Analist   | Liliana       | Richardson       | 7000      |
| Mobil Uygulama | Yazılımcı | Victoria      | Jones            | 3000      |
| Mobil Uygulama | Analist   | Luna          | Howard           | 6000      |
