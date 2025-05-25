---
title:  "Oracle - MONTHS_BETWEEN Fonksiyonu"
date: 2025-05-25 15:45:00 +0300
layout: post
categories: oracle
---

- `MONTHS_BETWEEN` fonksiyonu, iki tarih arasındaki ay farkını `NUMBER` tipinde döndürür.
- Dönüş değeri pozitif, negatif veya sıfır olabilir.
- Hesaplama `birinci tarih` - `ikinci tarih` şeklinde yapılır.
- Bir ayın 31 günden oluştuğu kabulüyle, kesirli hesaplama yapılır. Her iki tarihin de gün numarası aynıysa sonuç tam sayı olur.

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
| `MONTHS_BETWEEN(TO_DATE('01.03.2025', 'DD.MM.YYYY'), TO_DATE('28.02.2025', 'DD.MM.YYYY'))` | 0.129032258 (4 / 31)                 |
| `MONTHS_BETWEEN(TO_DATE('01.03.2025', 'DD.MM.YYYY'), TO_DATE('27.02.2025', 'DD.MM.YYYY'))` | 0.161290323 (5 / 31)                 |
| `MONTHS_BETWEEN(TO_DATE('30.04.2025', 'DD.MM.YYYY'), TO_DATE('31.05.2025', 'DD.MM.YYYY'))` | -1                                   |
| `MONTHS_BETWEEN(TO_DATE('30.04.2025', 'DD.MM.YYYY'), TO_DATE('01.05.2025', 'DD.MM.YYYY'))` | -0.06451613 (2 / 31)                 |
| `MONTHS_BETWEEN(TO_DATE('29.04.2025', 'DD.MM.YYYY'), TO_DATE('01.05.2025', 'DD.MM.YYYY'))` | -0.09677419 (3 / 31)                 |
| `MONTHS_BETWEEN(TO_DATE('19.05.2025', 'DD.MM.YYYY'), TO_DATE('19.05.2025', 'DD.MM.YYYY'))` | 0                                    |
| `MONTHS_BETWEEN(TO_DATE('20.05.2025', 'DD.MM.YYYY'), TO_DATE('19.05.2025', 'DD.MM.YYYY'))` | 0.032258065 (1/31)                   |
| `MONTHS_BETWEEN(TO_DATE('20.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), TO_DATE('19.05.2025 14:37:48', 'DD.MM.YYYY HH24:MI:SS'))` | 0.034946237 ((1 / 31) + (2 / 24 / 31)) |
