---
title:  "Oracle - TZ_OFFSET Fonksiyonu"
date: 2025-05-31 17:00:00 +0300
layout: post
categories: oracle
---

`TZ_OFFSET` fonksiyonu, bir zaman diliminin `UTC` zaman dilimiyle olan zaman farkını verir.

| Syntax                    |
|---------------------------|
| `TZ_OFFSET(zaman_dilimi)` |

- `zaman_dilimi` parametresi, `time zone offset ([+|-]TZH:TZM)` veya `zaman dilimi adı` olarak iki farklı formatta olabilir.

---

Aşağıdaki tabloda `TZ_OFFSET` fonksiyonu için kullanılabilecek formatlar ve açıklamaları yer almaktadır.

| Kullanım                       | Sonuç  |
|--------------------------------|--------|
| `TZ_OFFSET('Europe/Istanbul')` | +03:00 |
| `TZ_OFFSET('Europe/Paris')`    | +02:00 |
| `TZ_OFFSET('03:00')`           | +03:00 |
| `TZ_OFFSET('+03:00')`          | +03:00 |
| `TZ_OFFSET('02:00')`           | +02:00 |
| `TZ_OFFSET('+02:00')`          | +02:00 |
| `TZ_OFFSET('-04:00')`          | -04:00 |
| `TZ_OFFSET(SESSIONTIMEZONE)`   | +02:00 |
| `TZ_OFFSET(DBTIMEZONE)`        | -04:00 |
