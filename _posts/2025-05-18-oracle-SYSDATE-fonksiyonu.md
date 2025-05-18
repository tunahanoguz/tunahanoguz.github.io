---
title:  "Oracle - SYSDATE Fonksiyonu"
date: 2025-05-18 10:55:00 +0300
layout: post
categories: oracle
---

- `SYSDATE` fonksiyonu, sistemin tarih ve saat bilgisini `DATE` tipinde dönen bir fonksiyondur.
- Parametre almaz.
- Bu fonksiyonun döndüğü tarihin formatı, `NLS_DATE_FORMAT` adındaki oturum veya veritabanı düzeyinde belirlenebilen bir parametrenin değerine göre değişmektedir.

Aşağıdaki tabloda farklı `NLS_DATE_FORMAT` değerleriyle elde edilebilecek `SYSDATE` sonuçları bulunmaktadır.
Örnekler çoğaltılabilir. İhtiyaca uygun farklı kullanımlar her zaman için mümkündür.

| NLS_DATE_FORMAT         | Sonuç               |
|-------------------------|---------------------|
| `DD`                    | 18                  |
| `MM`                    | 05                  |
| `YYYY`                  | 2025                |
| `HH24`                  | 10                  |
| `MI`                    | 47                  |
| `SS`                    | 38                  |
| `DD.MM.YYYY`            | 18.05.2025          |
| `DD.MM.YYYY HH24`       | 18.05.2025 10       |
| `DD.MM.YYYY HH24:MI`    | 18.05.2025 10:47    |
| `DD.MM.YYYY HH24:MI:SS` | 18.05.2025 10:47:38 |
