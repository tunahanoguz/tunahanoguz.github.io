---
title:  "Oracle - SYSTIMESTAMP Fonksiyonu"
date: 2025-05-18 12:15:00 +0300
layout: post
categories: oracle
---

- `SYSTIMESTAMP` fonksiyonu, sistemin tarih ve saat bilgisini [`TIMESTAMP WITH TIME ZONE`]({% post_url 2025-05-17-oracle-DATE-ve-TIMESTAMP-veri-tipleri %}#TIMESTAMP-WITH-TIME-ZONE) tipinde döner.
- Parametre almaz.
- Bu fonksiyonun dönüş formatı, `NLS_TIMESTAMP_TZ_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| Syntax                                                       |
|--------------------------------------------------------------|
| ```SYSTIMESTAMP [AT TIME ZONE '+TZH:TZM' | 'zone1/zone2']``` |

| NLS_TIMESTAMP_TZ_FORMAT            | Kullanım                                      | Sonuç                             |
|------------------------------------|-----------------------------------------------|-----------------------------------|
| `DD`                               | `SYSTIMESTAMP`                                | 18                                |
| `MM`                               | `SYSTIMESTAMP`                                | 05                                |
| `YYYY`                             | `SYSTIMESTAMP`                                | 2025                              |
| `HH24`                             | `SYSTIMESTAMP`                                | 10                                |
| `MI`                               | `SYSTIMESTAMP`                                | 47                                |
| `SS`                               | `SYSTIMESTAMP`                                | 38                                |
| `FF`                               | `SYSTIMESTAMP`                                | 896496                            |
| `TZH`                              | `SYSTIMESTAMP`                                | +00                               |
| `TZM`                              | `SYSTIMESTAMP`                                | 00                                |
| `DD.MM.YYYY`                       | `SYSTIMESTAMP`                                | 18.05.2025                        |
| `DD.MM.YYYY HH24`                  | `SYSTIMESTAMP`                                | 18.05.2025 10                     |
| `DD.MM.YYYY HH24:MI`               | `SYSTIMESTAMP`                                | 18.05.2025 10:47                  |
| `DD.MM.YYYY HH24:MI:SS`            | `SYSTIMESTAMP`                                | 18.05.2025 10:47:38               |
| `DD.MM.YYYY HH24:MI:SS.FF`         | `SYSTIMESTAMP`                                | 18.05.2025 10:47:38.896496        |
| `DD.MM.YYYY HH24:MI:SS.FF TZH`     | `SYSTIMESTAMP`                                | 18.05.2025 10:47:38.896496 +00    |
| `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `SYSTIMESTAMP`                                | 18.05.2025 10:47:38.896496 +00:00 |
| `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `SYSTIMESTAMP AT TIME ZONE '+03:00'`          | 18.05.2025 13:47:38.896496 +03:00 |
| `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | `SYSTIMESTAMP AT TIME ZONE 'Europe/Istanbul'` | 18.05.2025 13:47:38.896496 +03:00 |
