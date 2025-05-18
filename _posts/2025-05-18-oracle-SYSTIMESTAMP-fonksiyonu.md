---
title:  "Oracle - SYSTIMESTAMP Fonksiyonu"
date: 2025-05-18 12:15:00 +0300
layout: post
categories: oracle
---

- `SYSTIMESTAMP` fonksiyonu, sistemin tarih ve saat bilgisini [`TIMESTAMP WITH TIME ZONE`]({% post_url 2025-05-17-oracle-DATE-ve-TIMESTAMP-veri-tipleri %}#TIMESTAMP-WITH-TIME-ZONE) tipinde döner.
- Parametre almaz.
- Bu fonksiyonun dönüş formatı, `NLS_TIMESTAMP_TZ_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| NLS_TIMESTAMP_TZ_FORMAT            | Sonuç                             |
|------------------------------------|-----------------------------------|
| `DD`                               | 18                                |
| `MM`                               | 05                                |
| `YYYY`                             | 2025                              |
| `HH24`                             | 10                                |
| `MI`                               | 47                                |
| `SS`                               | 38                                |
| `DD.MM.YYYY`                       | 18.05.2025                        |
| `DD.MM.YYYY HH24`                  | 18.05.2025 10                     |
| `DD.MM.YYYY HH24:MI`               | 18.05.2025 10:47                  |
| `DD.MM.YYYY HH24:MI:SS`            | 18.05.2025 10:47:38               |
| `DD.MM.YYYY HH24:MI:SS.FF`         | 18.05.2025 10:47:38.896496        |
| `DD.MM.YYYY HH24:MI:SS.FF TZH`     | 18.05.2025 10:47:38.896496 +00    |
| `DD.MM.YYYY HH24:MI:SS.FF TZH:TZM` | 18.05.2025 10:47:38.896496 +00:00 |
