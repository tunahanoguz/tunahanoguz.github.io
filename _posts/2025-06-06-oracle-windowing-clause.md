---
title:  "Oracle - Windowing Clause"
date: 2025-06-06 18:30:00 +0300
layout: post
categories: oracle
---

`WINDOWING CLAUSE`, analitik fonksiyonlara üzerinde çalışacağı kayıtlar için bir pencere/çerçeve çizilmesini sağlar. `ORDER BY CLAUSE` için eklenti görevi görür. Yalnızca `ORDER BY CLAUSE` varsa ve ilgili analitik fonksiyon destekliyorsa kullanılabilir.

İki basit formu vardır:
- `RANGE BETWEEN baslangic_noktasi AND bitis_noktasi`
- `ROWS BETWEEN baslangic_noktasi AND bitis_noktasi`

`RANGE` ifadesi, `ORDER BY CLAUSE` için belirtilen kolon(lar) veya ifade(ler)nin değer(ler)inin aynı olduğu durumlarda, analitik fonksiyonun o satırların tümünü hesaba katmasına sebep olur. Bu tür satırlar kendi aralarında bir `RANGE` (dizi/silsile) oluştururlar ve o `RANGE` içerisinde yer alan tüm satırlar için analitik fonksiyonun döndüğü değer aynı olur.

`ROWS` ifadesi ise, `ORDER BY CLAUSE` için belirtilen kolon(lar) veya ifade(ler)nin değeri aynı olsa bile, analitik fonksiyonun tüm satırları müstakil olarak değerlendirmesini sağlar.

`baslangic_noktasi` ifadesi, 3 farklı değer alabilir.
- `UNBOUNDED PRECEDING`: Analitik fonksiyonun hesaplamasına mevcut row/range'den önceki tüm row/rangelerin dahil edilmesini sağlar. Hesaplama ilk sıradaki row/range ile başlar.
- `CURRENT ROW`: Analitik fonksiyonun hesaplamaya mevcut row/range'den başlamasını sağlar.
- Üçüncü değer ise sabit bir sayı veya bir ifadenin sonucu olarak oluşan bir sayı olabilir. İlgili analitik fonksiyon hesaplamasına mevcut row/range'den bu sayı kadar öncesinde yer alan row/range'den başlar. Örneğin 1 değeri, mevcut row/range'den 1 önceki row/range'i ifade eder.

`bitis_noktasi` ifadesi de 3 farklı değer alabilir.
- `UNBOUNDED FOLLOWING`: İlgili analitik fonksiyonun hesaplamasına mevcut row/range'dan sonraki tüm row/rangelerin dahil edilmesini sağlar. Hesaplama ilk sıradaki row/range ile başlar.
- `CURRENT ROW`: İlgili analitik fonksiyonun hesaplamayı mevcut row/range ile bitirmesini sağlar.
- Üçüncü değer ise sabit bir sayı veya bir ifadenin sonucu olarak oluşan bir sayı olabilir. İlgili analitik fonksiyon hesaplamasını mevcut row/range'den bu sayı kadar sonra yer alan row/range ile bitirir. Örneğin 1 değeri, mevcut row/range'den 1 sonraki row/range'i ifade eder.

`WINDOWING CLAUSE` için varsayılan değer `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`'dur.

Aşağıdaki tabloda, `baslangic_noktasi` ve `bitis_noktasi` için örnek kullanımlar ve açıklamaları yer almaktadır.

| Kullanım                                                     | Açıklama                                                                                                                                                                                                                     |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```RANGE|ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW``` | İlgili analitik fonksiyon, hesaplamasına mevcut row/range'den önceki tüm row/range'leri dahil eder, hesaplamasına ilk sıradaki row/range ile başlar ve hesaplamasını mevcut row/range ile bitirir.                           |
| ```RANGE|ROWS BETWEEN UNBOUNDED PRECEDING AND 1 FOLLOWING``` | İlgili analitik fonksiyon, hesaplamasına mevcut row/range'den önceki tüm row/range'leri dahil eder, hesaplamasına ilk sıradaki row/range ile başlar ve hesaplamasını mevcut row/range'den bir sonraki row/range ile bitirir. |
| ```RANGE|ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING``` | İlgili analitik fonksiyon, hesaplamasına mevcut row/range ile başlar ve sonraki tüm row/rangeleri de sırasıyla hesaplamaya dahil eder.                                                                                       |
| ```RANGE|ROWS BETWEEN 1 PRECEDING AND UNBOUNDED FOLLOWING``` | İlgili analitik fonksiyon, hesaplamasına mevcut row/range'den bir önceki row/range ile başlar ve sonraki tüm row/rangeleri de sırasıyla hesaplamaya dahil eder.                                                              |
| ```RANGE|ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING```         | İlgili analitik fonksiyon, hesaplamasına mevcut row/range ile başlar ve hesaplamasını bir sonraki row/range ile bitirir.                                                                                                     |
| ```RANGE|ROWS BETWEEN 1 PRECEDING AND CURRENT ROW```         | İlgili analitik fonksiyon, hesaplamasına mevcut row/range'den bir önceki row/range ile başlar ve hesaplamasını mevcut row/range ile bitirir.                                                                                 |

---

Aşağıdaki tabloda örnek kullanımlar için kullanılacak veritabanı tablosundaki kayıtlar ve hangi kaydın kaçıncı range ve row olduğu bilgileri yer almaktadır.

| MUSTERIID | HARCAMATUTAR |     | ***Range No*** | ***Row No*** |
| --------- | ------------ | --- | -------------- | ------------ |
| 1         | 10           | -   | ***1***        | ***1***      |
| 2         | 20           | -   | ***2***        | ***2***      |
| 2         | 30           | -   | ***2***        | ***3***      |
| 3         | 40           | -   | ***3***        | ***4***      |
| 4         | 50           | -   | ***4***        | ***5***      |
| 4         | 60           | -   | ***4***        | ***6***      |
| 5         | 70           | -   | ***5***        | ***7***      |
| 6         | 80           | -   | ***6***        | ***8***      |

Aşağıdaki tabloda `WINDOWING CLAUSES` için kullanım örnekleri yer almaktadır. Sonuçlar yukarıdaki tabloda yer alan kayıtlara göre oluşturulmuştur.

| Kullanım                                                                                       |
| ---------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 10                    |
| 2         | 20           |     | 2         | 60                    |
| 2         | 30           |     | 2         | 60                    |
| 3         | 40           |     | 3         | 100                   |
| 4         | 50           |     | 4         | 210                   |
| 4         | 60           |     | 4         | 210                   |
| 5         | 70           |     | 5         | 280                   |
| 6         | 80           |     | 6         | 360                   |

---

| Kullanım                                                                                      |
| --------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 10                    |
| 2         | 20           |     | 2         | 30                    |
| 2         | 30           |     | 2         | 60                    |
| 3         | 40           |     | 3         | 100                   |
| 4         | 50           |     | 4         | 150                   |
| 4         | 60           |     | 4         | 210                   |
| 5         | 70           |     | 5         | 280                   |
| 6         | 80           |     | 6         | 360                   |

---

| Kullanım                                                                                       |
| ---------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN UNBOUNDED PRECEDING AND 1 FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 60                    |
| 2         | 20           |     | 2         | 100                   |
| 2         | 30           |     | 2         | 100                   |
| 3         | 40           |     | 3         | 210                   |
| 4         | 50           |     | 4         | 210                   |
| 4         | 60           |     | 4         | 210                   |
| 5         | 70           |     | 5         | 360                   |
| 6         | 80           |     | 6         | 360                   |

---

| Kullanım                                                                                      |
| --------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN UNBOUNDED PRECEDING AND 1 FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 30                    |
| 2         | 20           |     | 2         | 60                    |
| 2         | 30           |     | 2         | 100                   |
| 3         | 40           |     | 3         | 150                   |
| 4         | 50           |     | 4         | 210                   |
| 4         | 60           |     | 4         | 280                   |
| 5         | 70           |     | 5         | 360                   |
| 6         | 80           |     | 6         | 360                   |

---

| Kullanım                                                                                       |
| ---------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 360                   |
| 2         | 20           |     | 2         | 350                   |
| 2         | 30           |     | 2         | 350                   |
| 3         | 40           |     | 3         | 300                   |
| 4         | 50           |     | 4         | 260                   |
| 4         | 60           |     | 4         | 260                   |
| 5         | 70           |     | 5         | 150                   |
| 6         | 80           |     | 6         | 80                    |

---

| Kullanım                                                                                      |
| --------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 360                   |
| 2         | 20           |     | 2         | 350                   |
| 2         | 30           |     | 2         | 330                   |
| 3         | 40           |     | 3         | 300                   |
| 4         | 50           |     | 4         | 260                   |
| 4         | 60           |     | 4         | 210                   |
| 5         | 70           |     | 5         | 150                   |
| 6         | 80           |     | 6         | 80                    |

---

| Kullanım                                                                                       |
| ---------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN 1 PRECEDING AND UNBOUNDED FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 360                   |
| 2         | 20           |     | 2         | 360                   |
| 2         | 30           |     | 2         | 360                   |
| 3         | 40           |     | 3         | 350                   |
| 4         | 50           |     | 4         | 300                   |
| 4         | 60           |     | 4         | 300                   |
| 5         | 70           |     | 5         | 260                   |
| 6         | 80           |     | 6         | 150                   |

---

| Kullanım                                                                                      |
| --------------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN 1 PRECEDING AND UNBOUNDED FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 360                   |
| 2         | 20           |     | 2         | 360                   |
| 2         | 30           |     | 2         | 350                   |
| 3         | 40           |     | 3         | 330                   |
| 4         | 50           |     | 4         | 300                   |
| 4         | 60           |     | 4         | 260                   |
| 5         | 70           |     | 5         | 210                   |
| 6         | 80           |     | 6         | 150                   |

---

| Kullanım                                                                               |
| -------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN CURRENT ROW AND 1 FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 60                    |
| 2         | 20           |     | 2         | 90                    |
| 2         | 30           |     | 2         | 90                    |
| 3         | 40           |     | 3         | 150                   |
| 4         | 50           |     | 4         | 180                   |
| 4         | 60           |     | 4         | 180                   |
| 5         | 70           |     | 5         | 150                   |
| 6         | 80           |     | 6         | 80                    |

---

| Kullanım                                                                              |
| ------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 30                    |
| 2         | 20           |     | 2         | 50                    |
| 2         | 30           |     | 2         | 70                    |
| 3         | 40           |     | 3         | 90                    |
| 4         | 50           |     | 4         | 110                   |
| 4         | 60           |     | 4         | 130                   |
| 5         | 70           |     | 5         | 150                   |
| 6         | 80           |     | 6         | 80                    |


---

| Kullanım                                                                               |
| -------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID RANGE BETWEEN 1 PRECEDING AND CURRENT ROW)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 10                    |
| 2         | 20           |     | 2         | 60                    |
| 2         | 30           |     | 2         | 60                    |
| 3         | 40           |     | 3         | 90                    |
| 4         | 50           |     | 4         | 150                   |
| 4         | 60           |     | 4         | 150                   |
| 5         | 70           |     | 5         | 180                   |
| 6         | 80           |     | 6         | 150                   |

---

| Kullanım                                                                              |
| ------------------------------------------------------------------------------------- |
| `SUM(HARCAMATUTAR) OVER(ORDER BY MUSTERIID ROWS BETWEEN 1 PRECEDING AND CURRENT ROW)` |

| MUSTERIID | HARCAMATUTAR |     | MUSTERIID | SUM(HARCAMATUTAR) ... |
| --------- | ------------ | --- | --------- | --------------------- |
| 1         | 10           |     | 1         | 10                    |
| 2         | 20           |     | 2         | 30                    |
| 2         | 30           |     | 2         | 50                    |
| 3         | 40           |     | 3         | 70                    |
| 4         | 50           |     | 4         | 90                    |
| 4         | 60           |     | 4         | 110                   |
| 5         | 70           |     | 5         | 130                   |
| 6         | 80           |     | 6         | 150                   |
