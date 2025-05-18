---
title:  "Oracle - CURRENT_DATE Fonksiyonu"
date: 2025-05-18 11:15:00 +0300
layout: post
categories: oracle
---

- `CURRENT_DATE` fonksiyonu, kullanıcı oturumunda ayarlanmış `TIME_ZONE` parametresine göre, tarih ve saat bilgisini DATE tipinde döner.
- Parametre almaz.
- Bu fonksiyonun döndüğü tarihin formatı, `NLS_DATE_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| Time Zone | Format                  | Kullanım                         | Sonuç               |
|-----------|-------------------------|----------------------------------|---------------------|
| `+3:0`    | `DD`                    | `SELECT CURRENT_DATE FROM DUAL;` | 18                  |
| `+3:0`    | `MM`                    | `SELECT CURRENT_DATE FROM DUAL;` | 05                  |
| `+3:0`    | `YYYY`                  | `SELECT CURRENT_DATE FROM DUAL;` | 2025                |
| `+3:0`    | `HH24`                  | `SELECT CURRENT_DATE FROM DUAL;` | 10                  |
| `+3:0`    | `MI`                    | `SELECT CURRENT_DATE FROM DUAL;` | 47                  |
| `+3:0`    | `SS`                    | `SELECT CURRENT_DATE FROM DUAL;` | 38                  |
| `+3:0`    | `DD.MM.YYYY`            | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025          |
| `+3:0`    | `DD.MM.YYYY HH24`       | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10       |
| `+3:0`    | `DD.MM.YYYY HH24:MI`    | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10:47    |
| `+3:0`    | `DD.MM.YYYY HH24:MI:SS` | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10:47:38 |
