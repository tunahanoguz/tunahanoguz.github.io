---
title:  "Oracle - MONTHS_BETWEEN Fonksiyonu"
date: 2025-05-25 15:45:00 +0300
layout: post
categories: oracle
---

- `MONTHS_BETWEEN` fonksiyonu, iki tarih arasındaki ay farkını `NUMBER` tipinde döndürür.
- Dönüş değeri pozitif, negatif veya sıfır olabilir.
- Hesaplama `birinci tarih` - `ikinci tarih` şeklinde yapılır.
- Bir ayın 31 günden oluştuğu kabulüyle, kesirli hesaplama yapılır. Her iki tarihin de ayın ilk günü veya son günü olması durumunda sonuç tam sayı olur.

| Syntax                                        |
|-----------------------------------------------|
| `MONTHS_BETWEEN(birinci_tarih, ikinci_tarih)` |

---

- Aşağıdaki tabloda `MONTHS_BETWEEN` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım                                                                                   | Sonuç                                |
|--------------------------------------------------------------------------------------------|--------------------------------------|
| `MONTHS_BETWEEN(TO_DATE('01.05.2025', 'DD.MM.YYYY'), TO_DATE('01.06.2025', 'DD.MM.YYYY'))` | -1                                   |
| `MONTHS_BETWEEN(TO_DATE('01.05.2025', 'DD.MM.YYYY'), TO_DATE('01.04.2025', 'DD.MM.YYYY'))` | 1                                    |
| `MONTHS_BETWEEN(TO_DATE('31.05.2025', 'DD.MM.YYYY'), TO_DATE('30.06.2025', 'DD.MM.YYYY'))` | -1                                   |
| `MONTHS_BETWEEN(TO_DATE('31.05.2025', 'DD.MM.YYYY'), TO_DATE('30.04.2025', 'DD.MM.YYYY'))` | 1                                    |
| `MONTHS_BETWEEN(TO_DATE('31.05.2025', 'DD.MM.YYYY'), TO_DATE('29.06.2025', 'DD.MM.YYYY'))` | -0.93548387 (29 / 31)                |
| `MONTHS_BETWEEN(TO_DATE('01.05.2025', 'DD.MM.YYYY'), TO_DATE('29.04.2025', 'DD.MM.YYYY'))` | 0.096774194 ((31 - 29 + 1) / 31)     |
| `MONTHS_BETWEEN(TO_DATE('29.04.2025', 'DD.MM.YYYY'), TO_DATE('31.05.2025', 'DD.MM.YYYY'))` | -1.0645161 ((31 - 29 + 1) + 30) / 31 |
