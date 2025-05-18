---
title:  "Oracle - CURRENT_DATE Fonksiyonu"
date: 2025-05-18 11:15:00 +0300
layout: post
categories: oracle
---

- `CURRENT_DATE` fonksiyonu, kullanıcı oturumunda ayarlanmış `TIME_ZONE` parametresine göre, tarih ve saat bilgisini DATE tipinde döner.
- Parametre almaz.
- Bu fonksiyonun döndüğü tarihin formatı, `NLS_DATE_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

| Time Zone | Format                  | Sonuç               |
|-----------|-------------------------|---------------------|
| `+3:0`    | `DD`                    | 18                  |
| `+3:0`    | `MM`                    | 05                  |
| `+3:0`    | `YYYY`                  | 2025                |
| `+3:0`    | `HH24`                  | 10                  |
| `+3:0`    | `MI`                    | 47                  |
| `+3:0`    | `SS`                    | 38                  |
| `+3:0`    | `DD.MM.YYYY`            | 18.05.2025          |
| `+3:0`    | `DD.MM.YYYY HH24`       | 18.05.2025 10       |
| `+3:0`    | `DD.MM.YYYY HH24:MI`    | 18.05.2025 10:47    |
| `+3:0`    | `DD.MM.YYYY HH24:MI:SS` | 18.05.2025 10:47:38 |
