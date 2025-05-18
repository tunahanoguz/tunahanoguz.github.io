---
title:  "Oracle - CURRENT_TIMESTAMP Fonksiyonu"
date: 2025-05-18 14:45:00 +0300
layout: post
categories: oracle
---

- `CURRENT_TIMESTAMP` fonksiyonu, kullanıcı oturumunda belirlenmiş `TIME_ZONE` parametresine göre `TIMESTAMP WITH TIME ZONE` tipinde tarih ve saat bilgisini verir.
- Parametre almaz.
- Bu fonksiyonun dönüş formatı, `NLS_TIMESTAMP_TZ_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.
- `AT TIME ZONE` ile ayrıca bir time zone belirtilirse, kullanıcı oturumunda belirlenmiş `TIME_ZONE` parametresi ezilir.

| Syntax                                                            |
|-------------------------------------------------------------------|
| ```CURRENT_TIMESTAMP [AT TIME ZONE '+TZH:TZM' | 'zone1/zone2']``` |

Aşağıdaki tabloda farklı format ve kullanımlara göre elde edilecek sonuçlar bulunmaktadır.

| TIME_ZONE | NLS_TIMESTAMP_TZ_FORMAT            | Kullanım                                           | Sonuç                             |
|-----------|------------------------------------|----------------------------------------------------|-----------------------------------|
| `+0:0`    | `DD`                               | `CURRENT_TIMESTAMP`                                | 18                                |
| `+0:0`    | `MM`                               | `CURRENT_TIMESTAMP`                                | 05                                |
| `+0:0`    | `YYYY`                             | `CURRENT_TIMESTAMP`                                | 2025                              |
| `+0:0`    | `HH24`                             | `CURRENT_TIMESTAMP`                                | 10                                |
| `+0:0`    | `MI`                               | `CURRENT_TIMESTAMP`                                | 47                                |
| `+0:0`    | `SS`                               | `CURRENT_TIMESTAMP`                                | 38                                |
| `+0:0`    | `FF`                               | `CURRENT_TIMESTAMP`                                | 896496                            |
| `+0:0`    | `TZH`                              | `CURRENT_TIMESTAMP`                                | +00                               |
| `+0:0`    | `TZM`                              | `CURRENT_TIMESTAMP`                                | 00                                |
| `+0:0`    | `DD.MM.YYYY`                       | `CURRENT_TIMESTAMP`                                | 18.05.2025                        |
| `+0:0`    | `DD.MM.YYYY HH24`                  | `CURRENT_TIMESTAMP`                                | 18.05.2025 10                     |
| `+0:0`    | `DD.MM.YYYY HH24:MI`               | `CURRENT_TIMESTAMP`                                | 18.05.2025 10:47                  |
| `+0:0`    | `DD.MM.YYYY HH24:MI:SS`            | `CURRENT_TIMESTAMP`                                | 18.05.2025 10:47:38               |
| `+0:0`    | `DD.MM.YYYY HH24:MI:SS.FF`         | `CURRENT_TIMESTAMP`                                | 18.05.2025 10:47:38.896496        |
| `+0:0`    | `DD.MM.YYYY HH24:MI:SS.FF TZH`     | `CURRENT_TIMESTAMP`                                | 18.05.2025 10:47:38.896496 +00    |
| `+0:0`    | `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `CURRENT_TIMESTAMP`                                | 18.05.2025 10:47:38.896496 +00:00 |
| `+0:0` *(eziliyor)*    | `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `CURRENT_TIMESTAMP AT TIME ZONE '+03:00'`          | 18.05.2025 13:47:38.896496 +03:00 |
| `+0:0` *(eziliyor)*    | `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `CURRENT_TIMESTAMP AT TIME ZONE 'Europe/Istanbul'` | 18.05.2025 13:47:38.896496 +03:00 |
| `+3:0`    | `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `CURRENT_TIMESTAMP AT TIME ZONE '+03:00'`          | 18.05.2025 13:47:38.896496 +03:00 |
| `+3:0`    | `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `CURRENT_TIMESTAMP AT TIME ZONE 'Europe/Istanbul'` | 18.05.2025 13:47:38.896496 +03:00 |
