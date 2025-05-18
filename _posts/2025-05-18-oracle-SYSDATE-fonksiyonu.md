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

| Format                                      | Kullanım                    | Sonuç               |
|---------------------------------------------|-----------------------------|---------------------|
| `NLS_DATE_FORMAT = "DD"`                    | `SELECT SYSDATE FROM DUAL;` | 18                  |
| `NLS_DATE_FORMAT = "MM"`                    | `SELECT SYSDATE FROM DUAL;` | 05                  |
| `NLS_DATE_FORMAT = "YYYY"`                  | `SELECT SYSDATE FROM DUAL;` | 2025                |
| `NLS_DATE_FORMAT = "HH24"`                  | `SELECT SYSDATE FROM DUAL;` | 10                  |
| `NLS_DATE_FORMAT = "MI"`                    | `SELECT SYSDATE FROM DUAL;` | 47                  |
| `NLS_DATE_FORMAT = "SS"`                    | `SELECT SYSDATE FROM DUAL;` | 38                  |
| `NLS_DATE_FORMAT = "DD.MM.YYYY"`            | `SELECT SYSDATE FROM DUAL;` | 18.05.2025          |
| `NLS_DATE_FORMAT = "DD.MM.YYYY HH24"`       | `SELECT SYSDATE FROM DUAL;` | 18.05.2025 10       |
| `NLS_DATE_FORMAT = "DD.MM.YYYY HH24:MI"`    | `SELECT SYSDATE FROM DUAL;` | 18.05.2025 10:47    |
| `NLS_DATE_FORMAT = "DD.MM.YYYY HH24:MI:SS"` | `SELECT SYSDATE FROM DUAL;` | 18.05.2025 10:47:38 |
