---
title: "Oracle - CUME_DIST Fonksiyonu"
date: 2025-06-21 15:30:00 +0300
layout: post
categories: oracle
---

`CUME_DIST` fonksiyonu, belirli bir satır veya değer için, **kendisi de dahil olmak üzere**, kendisine eşit veya kendisinden daha küçük sıra/derece/rütbe numarasına (rank) sahip satır sayısını tüm satır sayısına böler ve sonucu döner.

| #   | HARCAMATUTARI | RANK | CUME_DIST |
| --- | ------------- | ---- | --------- |
| 1   | 3000          | 1    | 0.2       |
| 2   | 3000          | 1    | 0.2       |
| 3   | 4000          | 3    | 0.3       |
| 4   | 5000          | 4    | 0.4       |
| 5   | 6000          | 5    | 0.5       |
| 6   | 7000          | 6    | 0.7       |
| 7   | 7000          | 6    | 0.7       |
| 8   | 8000          | 8    | 0.8       |
| 9   | 9000          | 9    | 0.9       |
| 10  | 10000         | 10   | 1         |

---

## Syntax

| Aggregate/Analytic | Syntax                                                                                        |
| ------------------ | --------------------------------------------------------------------------------------------- |
| Aggregate          | `CUME_DIST(expr1 [, expr2, ... expr_n]) WITHIN GROUP (ORDER BY expr1 [, expr_2, ... expr_n])` |
| Analytic           | `CUME_DIST() OVER([query_partition_clause] ORDER BY clause)`                                  |

`CUME_DIST` fonksiyonu, hem `aggregate function` hem de `analytic function` olarak kullanılabilir. `Aggregate function` ve `analytic function` hakkında genel bilgilere [buradan]({% post_url 2025-06-06-oracle-aggregate-function-vs-analytic-function %} "Oracle - Aggregate Function vs Analytic Function") ulaşılabilir. İki kullanım da syntax ve çalışma davranışı bakımından farklılaşmaktadır.

`Analytic function` olarak kullanıldığında sadece `query_partition_clause` (opsiyonel) ve `ORDER BY clause` (zorunlu) üzerinden sıra/derece/rütbe numarası döner. Ayrıca herhangi bir kolon/ifade belirtilmez.

`Aggregate function` olarak kullanıldığında bir kolon ve ifade için, mevcut kolon ve ifadeler arasına eklendiğinde `ORDER BY clause` (zorunlu) üzerinden hangi sıra/derece/rütbe numarasının oluşacağını döner.

---

## `Analytic Function` Olarak Kullanımı İçin Örnekler

Aşağıda örnek sorgularda kullanılan `SATISLAR` tablosundaki kayıtlar yer almaktadır.

| #   | MUSTERIID | HARCAMATUTARI |
| --- | --------- | ------------- |
| 1   | 1         | 3000          |
| 2   | 1         | 4000          |
| 3   | 2         | 5000          |
| 4   | 3         | 6000          |
| 5   | 4         | 7000          |
| 6   | 5         | 8000          |
| 7   | 5         | 9000          |
| 8   | 5         | NULL          |
| 9   | 6         | 9000          |
| 10  | 7         | 10000         |

<br>

```sql
SELECT  MUSTERIID,
    	HARCAMATUTARI,
    	CUME_DIST() OVER(ORDER BY HARCAMATUTARI)
FROM SATISLAR
ORDER BY HARCAMATUTARI;
```

| MUSTERIID | HARCAMATUTARI | CUME_DIST() ... |
| --------- | ------------- | --------------- |
| 1         | 3000          | 0.1             |
| 1         | 4000          | 0.2             |
| 2         | 5000          | 0.3             |
| 3         | 6000          | 0.4             |
| 4         | 7000          | 0.5             |
| 5         | 8000          | 0.6             |
| 5         | 9000          | 0.8             |
| 6         | 9000          | 0.8             |
| 7         | 10000         | 0.9             |
| 5         | NULL          | 1               |

<br>

```sql
SELECT  MUSTERIID,
    	HARCAMATUTARI,
    	CUME_DIST() OVER(ORDER BY HARCAMATUTARI DESC)
FROM SATISLAR
ORDER BY HARCAMATUTARI DESC;
```

| MUSTERIID | HARCAMATUTARI | CUME_DIST() ... |
| --------- | ------------- | --------------- |
| 5         | NULL          | 0.1             |
| 7         | 10000         | 0.2             |
| 6         | 9000          | 0.4             |
| 5         | 9000          | 0.4             |
| 5         | 8000          | 0.5             |
| 4         | 7000          | 0.6             |
| 3         | 6000          | 0.7             |
| 2         | 5000          | 0.8             |
| 1         | 4000          | 0.9             |
| 1         | 3000          | 1               |

<br>

```sql
SELECT  MUSTERIID,
    	HARCAMATUTARI,
    	CUME_DIST() OVER(PARTITION BY MUSTERIID ORDER BY HARCAMATUTARI)
FROM SATISLAR
ORDER BY MUSTERIID, HARCAMATUTARI;
```

| MUSTERIID | HARCAMATUTARI | CUME_DIST() ... |
| --------- | ------------- | --------------- |
| 1         | 3000          | 0.5             |
| 1         | 4000          | 1               |
| 2         | 5000          | 1               |
| 3         | 6000          | 1               |
| 4         | 7000          | 1               |
| 5         | 8000          | 0.3333333333    |
| 5         | 9000          | 0.6666666667    |
| 5         | NULL          | 1               |
| 6         | 9000          | 1               |
| 7         | 10000         | 1               |

<br>

```sql
SELECT  MUSTERIID,
    	HARCAMATUTARI,
    	CUME_DIST() OVER(PARTITION BY MUSTERIID ORDER BY HARCAMATUTARI DESC)
FROM SATISLAR
ORDER BY MUSTERIID, HARCAMATUTARI DESC;
```

| MUSTERIID | HARCAMATUTARI | CUME_DIST() ... |
| --------- | ------------- | --------------- |
| 1         | 4000          | 0.5             |
| 1         | 3000          | 1               |
| 2         | 5000          | 1               |
| 3         | 6000          | 1               |
| 4         | 7000          | 1               |
| 5         | NULL          | 0.3333333333    |
| 5         | 9000          | 0.6666666667    |
| 5         | 8000          | 1               |
| 6         | 9000          | 1               |
| 7         | 10000         | 1               |

---

## `Aggregate Function` Olarak Kullanımı İçin Örnekler


| #   | MUSTERIID | HARCAMATUTARI |
| --- | --------- | ------------- |
| 1   | 1         | 3000          |
| 2   | 1         | 4000          |
| 3   | 2         | 5000          |
| 4   | 3         | 6000          |
| 5   | 4         | 7000          |
| 6   | 5         | 8000          |
| 7   | 5         | 9000          |
| 8   | 5         | NULL          |
| 9   | 6         | 9000          |
| 10  | 7         | 10000         |

| Kullanım                                         | Sonuç                                 |
| ------------------------------------------------ | ------------------------------------- |
| `CUME_DIST(1000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.0909090909 (1/11)                   |
| `CUME_DIST(2000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.0909090909 (1/11)                   |
| `CUME_DIST(3000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.1818181818 (2/11)                   |
| `CUME_DIST(4000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.2727272727 (3/11)                   |
| `CUME_DIST(5000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.3636363636 (4/11)                   |
| `CUME_DIST(6000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.4545454545 (5/11)                   |
| `CUME_DIST(7000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.5454545454 (6/11)                   |
| `CUME_DIST(8000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.6363636364 (7/11)                   |
| `CUME_DIST(9000) WITHIN GROUP (ORDER BY TUTAR)`  | 0.8181818182 (9/11)                   |
| `CUME_DIST(10000) WITHIN GROUP (ORDER BY TUTAR)` | 0.9090909091 (10/11)                  |
| `CUME_DIST(11000) WITHIN GROUP (ORDER BY TUTAR)` | 0.9090909091 (10/11) (Son değer NULL) |
| `CUME_DIST(NULL) WITHIN GROUP (ORDER BY TUTAR)`  | 1                                     |

<br>

| #   | MUSTERIID | HARCAMATUTARI |
| --- | --------- | ------------- |
| 1   | 5         | NULL          |
| 2   | 7         | 10000         |
| 3   | 6         | 9000          |
| 4   | 5         | 9000          |
| 5   | 5         | 8000          |
| 6   | 4         | 7000          |
| 7   | 3         | 6000          |
| 8   | 2         | 5000          |
| 9   | 1         | 4000          |
| 10  | 1         | 3000          |

| Kullanım                                              | Sonuç                |
| ----------------------------------------------------- | -------------------- |
| `CUME_DIST(1000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 1                    |
| `CUME_DIST(2000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 1                    |
| `CUME_DIST(3000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 1                    |
| `CUME_DIST(4000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.9090909091 (10/11) |
| `CUME_DIST(5000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.8181818182 (9/11)  |
| `CUME_DIST(6000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.7272727273 (8/11)  |
| `CUME_DIST(7000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.6363636364(7/11)   |
| `CUME_DIST(8000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.5454545455 (6/11)  |
| `CUME_DIST(9000) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.4545454545 (5/11)  |
| `CUME_DIST(10000) WITHIN GROUP (ORDER BY TUTAR DESC)` | 0.2727272727 (3/11)  |
| `CUME_DIST(11000) WITHIN GROUP (ORDER BY TUTAR DESC)` | 0.1818181818 (2/11)  |
| `CUME_DIST(NULL) WITHIN GROUP (ORDER BY TUTAR DESC)`  | 0.1818181818 (2/11)  |

<br>

| #   | MUSTERIID | HARCAMATUTARI |
| --- | --------- | ------------- |
| 1   | 1         | 3000          |
| 2   | 1         | 4000          |
| 3   | 2         | 5000          |
| 4   | 3         | 6000          |
| 5   | 4         | 7000          |
| 6   | 5         | 8000          |
| 7   | 5         | 9000          |
| 8   | 5         | NULL          |
| 9   | 6         | 9000          |
| 10  | 7         | 10000         |

| Kullanım                                                       | Sonuç                |
| -------------------------------------------------------------- | -------------------- |
| `CUME_DIST(1, 2000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.0909090909 (1/11)  |
| `CUME_DIST(1, 3000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.1818181818 (2/11)  |
| `CUME_DIST(1, 4000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.2727272727 (3/11)  |
| `CUME_DIST(1, 5000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.2727272727 (3/11)  |
| `CUME_DIST(1, 6000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.2727272727 (3/11)  |
| `CUME_DIST(2, 4000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.2727272727 (3/11)  |
| `CUME_DIST(2, 5000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.3636363636 (4/11)  |
| `CUME_DIST(2, 6000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.3636363636 (4/11)  |
| `CUME_DIST(5, NULL) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.8181818182 (9/11)  |
| `CUME_DIST(7, 9000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)`  | 0.9090909091 (10/11) |
| `CUME_DIST(7, 10000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)` | 1 (11/11)            |
| `CUME_DIST(7, 11000) WITHIN GROUP (ORDER BY MUSTERIID, TUTAR)` | 1 (11/11)            |
