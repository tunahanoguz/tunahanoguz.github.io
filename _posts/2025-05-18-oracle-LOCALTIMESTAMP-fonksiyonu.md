---
title:  "Oracle - LOCALTIMESTAMP Fonksiyonu"
date: 2025-05-18 15:15:00 +0300
layout: post
categories: oracle
---

- `LOCALTIMESTAMP` fonksiyonu, kullanıcı oturumunda belirlenmiş `TIME_ZONE` parametresine göre `TIMESTAMP` tipinde tarih ve saat bilgisini verir.
- Parametre almaz.
- Bu fonksiyonun dönüş formatı, `NLS_TIMESTAMP_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.
- `AT TIME ZONE` ile ayrıca bir time zone belirtilirse, kullanıcı oturumunda belirlenmiş `TIME_ZONE` parametresi ezilir.
  - Bu durumda fonksiyonun döndüğü değerin tipi `TIMESTAMP WITH TIME ZONE` olarak değişir.
  - Bu değişimle birlikte dönüş formatı `NLS_TIMESTAMP_TZ_FORMAT` ile belirlenir.
- `LOCALTIMESTAMP` fonksiyonunun `CURRENT_TIMESTAMP` fonksiyonundan tek farkı,
  - `CURRENT_TIMESTAMP` fonksiyonunun `TIMESTAMP WITH TIME ZONE` tipinde,
  - `LOCALTIMESTAMP` fonksiyonunun ise `TIMESTAMP` tipinde değer dönmesidir.

| TIME_ZONE              | NLS_TIMESTAMP_[TZ_]FORMAT       | Kullanım                                        | Sonuç                             |
|------------------------|----------------------------|-------------------------------------------------|-----------------------------------|
| `+0:0`                 | `DD`                       | `LOCALTIMESTAMP`                                | 18                                |
| `+0:0`                 | `MM`                       | `LOCALTIMESTAMP`                                | 05                                |
| `+0:0`                 | `YYYY`                     | `LOCALTIMESTAMP`                                | 2025                              |
| `+0:0`                 | `HH24`                     | `LOCALTIMESTAMP`                                | 10                                |
| `+0:0`                 | `MI`                       | `LOCALTIMESTAMP`                                | 47                                |
| `+0:0`                 | `SS`                       | `LOCALTIMESTAMP`                                | 38                                |
| `+0:0`                 | `FF`                       | `LOCALTIMESTAMP`                                | 896496                            |
| `+0:0`                 | `TZH`                      | `LOCALTIMESTAMP`                                | +00                               |
| `+0:0`                 | `TZM`                      | `LOCALTIMESTAMP`                                | 00                                |
| `+0:0`                 | `DD.MM.YYYY`               | `LOCALTIMESTAMP`                                | 18.05.2025                        |
| `+0:0`                 | `DD.MM.YYYY HH24`          | `LOCALTIMESTAMP`                                | 18.05.2025 10                     |
| `+0:0`                 | `DD.MM.YYYY HH24:MI`       | `LOCALTIMESTAMP`                                | 18.05.2025 10:47                  |
| `+0:0`                 | `DD.MM.YYYY HH24:MI:SS`    | `LOCALTIMESTAMP`                                | 18.05.2025 10:47:38               |
| `+0:0`                 | `DD.MM.YYYY HH24:MI:SS.FF` | `LOCALTIMESTAMP`                                | 18.05.2025 10:47:38.896496        |
| `+0:0` *(eziliyor)*    | `DD.MM.YYYY HH24:MI:SS.FF` | `LOCALTIMESTAMP AT TIME ZONE '+03:00'`          | 18.05.2025 13:47:38.896496 +03:00 |
| `+0:0` *(eziliyor)*    | `DD.MM.YYYY HH24:MI:SS.FF` | `LOCALTIMESTAMP AT TIME ZONE 'Europe/Istanbul'` | 18.05.2025 13:47:38.896496 +03:00 |
| `+3:0`                 | `DD.MM.YYYY HH24:MI:SS.FF` | `LOCALTIMESTAMP AT TIME ZONE '+03:00'`          | 18.05.2025 13:47:38.896496 +03:00 |
| `+3:0`                 | `DD.MM.YYYY HH24:MI:SS.FF` | `LOCALTIMESTAMP AT TIME ZONE 'Europe/Istanbul'` | 18.05.2025 13:47:38.896496 +03:00 |
