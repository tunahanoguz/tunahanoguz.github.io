---
title:  "Oracle - SYSTIMESTAMP Fonksiyonu"
date: 2025-05-18 12:15:00 +0300
layout: post
categories: oracle
---

- `SYSTIMESTAMP` fonksiyonu, sistemin tarih ve saat bilgisini [`TIMESTAMP WITH TIME ZONE`]({% post_url 2025-05-17-oracle-DATE-ve-TIMESTAMP-veri-tipleri %}/#TIMESTAMP-WITH-TIME-ZONE) tipinde döner.
- Parametre almaz.
- Bu fonksiyonun dönüş formatı, `NLS_TIMESTAMP_TZ_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| NLS_TIMESTAMP_TZ_FORMAT | Sonuç               |
|-------------------------|---------------------|
| x                       | x                   |
