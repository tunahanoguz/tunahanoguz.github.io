---
title:  "Oracle - SYSDATE Fonksiyonu"
layout: post
categories: oracle
---

- `SYSDATE` fonksiyonu, sistemin tarih ve saat bilgisini `DATE` tipinde dönen bir fonksiyondur.
- Bu fonksiyonun döndüğü tarihin formatı `NLS_DATE_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| Kullanım `NLS_DATE_FORMAT = "DD.MM.YYYY HH24:MI:SS"` | Sonuç               |
|------------------------------------------------------|---------------------|
| `SELECT SYSDATE FROM DUAL;`                          | 18.05.2025 10:47:38 |
