---
title: "Oracle - RANK, DENSE_RANK ve PERCENT_RANK Fonksiyonu"
date: 2025-06-18 20:30:00 +0300
layout: post
categories: oracle
---

## 1. `RANK` Fonksiyonu

- `RANK` fonksiyonu, fonksiyon için belirtilen `ORDER BY clause` üzerinden her satır için bir sıra/derece/rütbe numarası döndürür.
- `ORDER BY clause` içerisinde yer alan kolon ve ifadeler aynı değerlere sahipse o satırlar için aynı sıra/derece/rütbe numarası dönecektir. Ancak, bir sonraki satır için sıra/derece/rütbe numarası çoklayan kayıt sayısı kadar atlanarak oluşturulur. Bu sebeple, `RANK` fonksiyonu ardışık sıra/derece/rütbe numaraları oluşturmayabilir.

| TUTAR (ascending sıralama) | RANK |
| -------------------------- | ---- |
| 10                         | 1    |
| 20                         | 2    |
| 30                         | 3    |
| 40                         | 4    |
| 40                         | 4    |
| 50                         | 6    |
| NULL                       | 7    |

<br>

| TUTAR (descending sıralama) | RANK |
| --------------------------- | ---- |
| NULL                        | 1    |
| 50                          | 2    |
| 40                          | 3    |
| 40                          | 3    |
| 30                          | 5    |
| 20                          | 6    |
| 10                          | 7    |

---

## 2. `DENSE_RANK` Fonksiyonu

`DENSE_RANK` fonksiyonunun `RANK` fonksiyondan tek farkı sıra/derece/rütbe numaralarında atlama olmamasıdır. Yani, `ORDER BY clause` içerisinde yer alan kolon ve ifadeler aynı değerlere olduğunda o satırlar için aynı sıra/derece/rütbe numarası oluşturulsa bile, farklı olan bir sonraki satırın sıra/derece/rütbe numarası ardışık olacak şekilde oluşturulur.

| TUTAR (ascending sıralama) | DENSE_RANK |
| -------------------------- | ---------- |
| 10                         | 1          |
| 20                         | 2          |
| 30                         | 3          |
| 40                         | 4          |
| 40                         | 4          |
| 50                         | 5          |
| NULL                       | 6          |

<br>

| TUTAR (descending sıralama) | RANK |
| --------------------------- | ---- |
| NULL                        | 1    |
| 50                          | 2    |
| 40                          | 3    |
| 40                          | 3    |
| 30                          | 4    |
| 20                          | 5    |
| 10                          | 6    |

---

## 3. `PERCENT_RANK` Fonksiyonu

`PERCENT_RANK` fonksiyonu, fonksiyon için belirtilen `ORDER BY clause` üzerinden her satır için o satırın kendi dışındaki kaç satırdan daha yüksek sıra/derece/rütbe numarasına sahip olduğunu yüzdesel olarak döndürür.

| TUTAR | RANK | DENSE_RANK | PERCENT_RANK | Açıklama                                                                                              |
| ----- | ---- | ---------- | ------------ | ----------------------------------------------------------------------------------------------------- |
| 10    | 1    | 1          | 0            | Bu satır, hiçbir satırdan daha yüksek sıra/derece/rütbe numarasına sahip değildir. (%0)               |
| 20    | 2    | 2          | 0.2          | Bu satır, kendı dışındaki 5 satırın 1'ünden daha yüksek sıra/derece/rütbe numarasına sahiptir. (%20)  |
| 30    | 3    | 3          | 0.4          | Bu satır, kendi dışındaki 5 satırın 2'sinden daha yüksek sıra/derece/rütbe numarasına sahiptir. (%40) |
| 40    | 4    | 4          | 0.6          | Bu satır, kendı dışındaki 5 satırın 3'ünden daha yüksek sıra/derece/rütbe numarasına sahiptir. (%60)  |
| 40    | 4    | 4          | 0.6          | Bu satır, kendı dışındaki 5 satırın 3'ünden daha yüksek sıra/derece/rütbe numarasına sahiptir. (%60)  |
| 50    | 6    | 5          | 1            | Bu satır, tüm satırlardan daha yüksek sıra/derece/rütbe numarasına sahiptir. (%100)                   |

---

## Aggregate ve Analytic Function Olarak Kullanım

| Aggregate/Analytic | Syntax                                                                                           |
| ------------------ | ------------------------------------------------------------------------------------------------ |
| Aggregate          | `RANK(expr1 [, expr2, ... expr_n]) WITHIN GROUP (ORDER BY expr1 [, expr_2, ... expr_n])`         |
| Analytic           | `RANK() OVER([query_partition_clause] ORDER BY clause)`                                          |
| Aggregate          | `DENSE_RANK(expr1 [, expr2, ... expr_n]) WITHIN GROUP (ORDER BY expr1 [, expr_2, ... expr_n])`   |
| Analytic           | `DENSE_RANK() OVER([query_partition_clause] ORDER BY clause)`                                    |
| Aggregate          | `PERCENT_RANK(expr1 [, expr2, ... expr_n]) WITHIN GROUP (ORDER BY expr1 [, expr_2, ... expr_n])` |
| Analytic           | `PERCENT_RANK() OVER([query_partition_clause] ORDER BY clause)`                                  |

Üç fonksiyon da hem `aggregate function` hem de `analytic function` olarak kullanılabilir. `Aggregate function` ve `analytic function` hakkında genel bilgilere [buradan]({% post_url 2025-06-06-oracle-aggregate-function-vs-analytic-function %} "Oracle - Aggregate Function vs Analytic Function") ulaşılabilir. Her iki kullanımda da syntax değişim göstermektedir.

`Analytic function` olarak kullanıldığında sadece `query_partition_clause` (opsiyonel) ve `ORDER BY clause` (zorunlu) üzerinden sıra/derece/rütbe numarası döner. Ayrıca herhangi bir kolon/ifade belirtilmez.

`Aggregate function` olarak kullanıldığında bir kolon ve ifade için, mevcut kolon ve ifadeler arasına eklendiğinde `ORDER BY clause` (zorunlu) üzerinden hangi sıra/derece/rütbe numarasının oluşacağını döner.

---

## `Analytic Function` Olarak Kullanım Örnekleri

Aşağıda örnek sorgularda kullanılan `SATISLAR` tablosundaki kayıtlar yer almaktadır.

| #   | KATEGORI   | TUTAR |
| --- | ---------- | ----- |
| 1   | Eğlence    | 40    |
| 2   | Elektronik | 10    |
| 3   | Elektronik | 60    |
| 4   | Gıda       | 20    |
| 5   | Giyim      | 30    |
| 6   | Giyim      | 50    |
| 7   | Sağlık     | 70    |
| 8   | Eğlence    | 40    |
| 9   | Gıda       | 80    |
| 10  | Eğlence    | 90    |

<br>

```sql
SELECT  TUTAR,
	RANK() OVER(ORDER BY TUTAR),
    	DENSE_RANK() OVER(ORDER BY TUTAR),
    	PERCENT_RANK() OVER(ORDER BY TUTAR)
FROM SATISLAR
ORDER BY TUTAR;
```

| #   | TUTAR | RANK | DENSE_RANK | PERCENT_RANK       |
| --- | ----- | ---- | ---------- | ------------------ |
| 1   | 10    | 1    | 1          | 0                  |
| 2   | 20    | 2    | 2          | 0.1111111111 (1/9) |
| 3   | 30    | 3    | 3          | 0.2222222222 (2/9) |
| 4   | 40    | 4    | 4          | 0.3333333333 (3/9) |
| 5   | 40    | 4    | 4          | 0.3333333333 (3/9) |
| 6   | 50    | 6    | 5          | 0.5555555556 (5/9) |
| 7   | 60    | 7    | 6          | 0.6666666667 (6/9) |
| 8   | 70    | 8    | 7          | 0.7777777778 (7/9) |
| 9   | 80    | 9    | 8          | 0.8888888889(8/9)  |
| 10  | 90    | 10   | 9          | 1                  |

<br>

```sql
SELECT  KATEGORI,
    	TUTAR,
    	RANK() OVER(PARTITION BY KATEGORI ORDER BY TUTAR),
    	DENSE_RANK() OVER(PARTITION BY KATEGORI ORDER BY TUTAR),
    	PERCENT_RANK() OVER(PARTITION BY KATEGORI ORDER BY TUTAR)
FROM SATISLAR
ORDER BY KATEGORI, TUTAR;
```

| #   | KATEGORI   | TUTAR | RANK | DENSE_RANK | PERCENT_RANK |
| --- | ---------- | ----- | ---- | ---------- | ------------ |
| 1   | Eğlence    | 40    | 1    | 1          | 0            |
| 2   | Eğlence    | 40    | 1    | 1          | 0            |
| 3   | Eğlence    | 90    | 3    | 2          | 1            |
| 4   | Elektronik | 10    | 1    | 1          | 0            |
| 5   | Elektronik | 60    | 2    | 2          | 1            |
| 6   | Gıda       | 20    | 1    | 1          | 0            |
| 7   | Gıda       | 80    | 2    | 2          | 1            |
| 8   | Giyim      | 30    | 1    | 1          | 0            |
| 9   | Giyim      | 50    | 2    | 2          | 1            |
| 10  | Sağlık     | 70    | 1    | 1          | 0            |

---

## `Aggregate Function` Olarak Kullanım Örnekleri

| Kullanım                                                      | Sonuç      |
| ------------------------------------------------------------- | ---------- |
| `RANK(10) WITHIN GROUP (ORDER BY TUTAR)`                      | 1          |
| `RANK(20) WITHIN GROUP (ORDER BY TUTAR)`                      | 2          |
| `RANK(30) WITHIN GROUP (ORDER BY TUTAR)`                      | 3          |
| `RANK(40) WITHIN GROUP (ORDER BY TUTAR)`                      | 4          |
| `RANK(50) WITHIN GROUP (ORDER BY TUTAR)`                      | 6          |
| `RANK(60) WITHIN GROUP (ORDER BY TUTAR)`                      | 7          |
| `RANK(70) WITHIN GROUP (ORDER BY TUTAR)`                      | 8          |
| `RANK(80) WITHIN GROUP (ORDER BY TUTAR)`                      | 9          |
| `RANK(90) WITHIN GROUP (ORDER BY TUTAR)`                      | 10         |
| `RANK(80, 'Eğlence') WITHIN GROUP (ORDER BY TUTAR, KATEGORI)` | 9          |
| `RANK(80, 'Spor') WITHIN GROUP (ORDER BY TUTAR, KATEGORI)`    | 10         |
| `DENSE_RANK(10) WITHIN GROUP (ORDER BY TUTAR)`                | 1          |
| `DENSE_RANK(20) WITHIN GROUP (ORDER BY TUTAR)`                | 2          |
| `DENSE_RANK(30) WITHIN GROUP (ORDER BY TUTAR)`                | 3          |
| `DENSE_RANK(40) WITHIN GROUP (ORDER BY TUTAR)`                | 4          |
| `DENSE_RANK(50) WITHIN GROUP (ORDER BY TUTAR)`                | 5          |
| `DENSE_RANK(60) WITHIN GROUP (ORDER BY TUTAR)`                | 6          |
| `DENSE_RANK(70) WITHIN GROUP (ORDER BY TUTAR)`                | 7          |
| `DENSE_RANK(80) WITHIN GROUP (ORDER BY TUTAR)`                | 8          |
| `DENSE_RANK(90) WITHIN GROUP (ORDER BY TUTAR)`                | 9          |
| `PERCENT_RANK(10) WITHIN GROUP (ORDER BY TUTAR)`              | 0          |
| `PERCENT_RANK(20) WITHIN GROUP (ORDER BY TUTAR)`              | 0.1 (1/10) |
| `PERCENT_RANK(30) WITHIN GROUP (ORDER BY TUTAR)`              | 0.2 (2/10) |
| `PERCENT_RANK(40) WITHIN GROUP (ORDER BY TUTAR)`              | 0.3 (3/10) |
| `PERCENT_RANK(50) WITHIN GROUP (ORDER BY TUTAR)`              | 0.5 (5/10) |
| `PERCENT_RANK(60) WITHIN GROUP (ORDER BY TUTAR)`              | 0.6 (6/10) |
| `PERCENT_RANK(70) WITHIN GROUP (ORDER BY TUTAR)`              | 0.7 (7/10) |
| `PERCENT_RANK(80) WITHIN GROUP (ORDER BY TUTAR)`              | 0.8 (8/10) |
| `PERCENT_RANK(90) WITHIN GROUP (ORDER BY TUTAR)`              | 0.9 (9/10) |
| `PERCENT_RANK(100) WITHIN GROUP (ORDER BY TUTAR)`             | 1 (10/10)  |
