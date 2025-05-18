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
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "DD"`                    | `SELECT CURRENT_DATE FROM DUAL;` | 18                  |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "MM"`                    | `SELECT CURRENT_DATE FROM DUAL;` | 05                  |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "YYYY"`                  | `SELECT CURRENT_DATE FROM DUAL;` | 2025                |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "HH24"`                  | `SELECT CURRENT_DATE FROM DUAL;` | 10                  |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "MI"`                    | `SELECT CURRENT_DATE FROM DUAL;` | 47                  |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "SS"`                    | `SELECT CURRENT_DATE FROM DUAL;` | 38                  |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "DD.MM.YYYY"`            | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025          |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "DD.MM.YYYY HH24"`       | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10       |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = "DD.MM.YYYY HH24:MI"`    | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10:47    |
| `TIME_ZONE = '+3:0'` | `NLS_DATE_FORMAT = 'DD.MM.YYYY HH24:MI:SS'` | `SELECT CURRENT_DATE FROM DUAL;` | 18.05.2025 10:47:38 |
