---
title:  "Oracle - ADD_MONTHS Fonksiyonu"
date: 2025-05-25 09:00:00 +0300
layout: post
categories: oracle
---

`ADD_MONTHS` fonksiyonu, `DATE`, `TIMESTAMP` ve `TIMESTAMP WITH TIME ZONE` tipinde bir tarihe belirtilen sayıda ay ekler ve yeni tarihi yine `DATE` tipinde döner.

| Syntax                         |
|--------------------------------|
| `ADD_MONTHS(tarih, ay_sayisi)` |

- `ay_sayisi` parametresi negatif bir sayı olarak verildiğinde o kadar ayı çıkarır.

---

- Aşağıdaki tabloda `ADD_MONTHS` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS AM BC` olarak belirlenmiştir.

| Kullanım                                                                                         | Sonuç                     |
|--------------------------------------------------------------------------------------------------|---------------------------|
| `ADD_MONTHS(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 1)`                                             | 19.06.2025 12:00:00 AM AD |
| `ADD_MONTHS(TO_DATE('19.05.2025', 'DD.MM.YYYY'), -1)`                                            | 19.04.2025 12:00:00 AM AD |
| `ADD_MONTHS(TO_DATE('31.05.2025', 'DD.MM.YYYY'), 1)`                                             | 30.06.2025 12:00:00 AM AD |
| `ADD_MONTHS(TO_DATE('31.05.2025', 'DD.MM.YYYY'), -1)`                                            | 30.04.2025 12:00:00 AM AD |
| `ADD_MONTHS(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 1)`                         | 19.06.2025 16:37:48 AM AD |
| `ADD_MONTHS(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), -1)`                        | 19.04.2025 16:37:48 AM AD |
| `ADD_MONTHS(TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 1)`                    | 19.06.2025 16:37:48 AM AD |
| `ADD_MONTHS(TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), -1)`                   | 19.04.2025 16:37:48 AM AD |
| `ADD_MONTHS(TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'), 1)`  | 19.06.2025 16:37:48 AM AD |
| `ADD_MONTHS(TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'), -1)` | 19.04.2025 16:37:48 AM AD |
