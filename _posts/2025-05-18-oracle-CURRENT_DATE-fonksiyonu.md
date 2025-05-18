---
title:  "Oracle - CURRENT_DATE Fonksiyonu"
date: 2025-05-18 11:15:00 +0300
layout: post
categories: oracle
---

- `CURRENT_DATE` fonksiyonu, kullanıcı oturumunda ayarlanmış time zone bilgisine göre, tarih ve saat bilgisini DATE tipinde döner.
- Parametre almaz.
- Bu fonksiyonun döndüğü tarihin formatı, `NLS_DATE_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| Time Zone            | Format                                      | Kullanım                         | Sonuç               |
|----------------------|---------------------------------------------|----------------------------------|---------------------|
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = 'DD.MM.YYYY HH24:MI:SS'` | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10:47:38 |
