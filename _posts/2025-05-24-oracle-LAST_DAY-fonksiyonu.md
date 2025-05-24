---
title:  "Oracle - LAST_DAY Fonksiyonu"
date: 2025-05-24 18:15:00 +0300
layout: post
categories: oracle
---

`LAST_DAY` fonksiyonu, bir tarihin bulunduğu ayın son gününü verir.

| Syntax            |
|-------------------|
| `LAST_DAY(tarih)` |

---

- Aşağıdaki tabloda `LAST_DAY` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS AM BC` olarak belirlenmiştir.

| Kullanım                                                            | Sonuç                     |
|---------------------------------------------------------------------|---------------------------|
| `LAST_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                     | 31.05.2025 12:00:00 AM AD |
| `LAST_DAY(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))` | 31.05.2025 16:37:48 AM AD |
