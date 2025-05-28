---
title:  "Oracle - TRUNC(datetime) Fonksiyonu"
date: 2025-05-27 20:30:00 +0300
layout: post
categories: oracle
---

- `TRUNC(datetime)` fonksiyonu, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir verinin belirtilen birim düzeyine kadar indirgenmesini sağlar.
- Örnek olarak, değeri yılın ilk gününe, ayın ilk gününe veya haftanın ilk gününe indirger.
- Zamanın belirli bir formatına odaklanmak için kullanışlı bir fonksiyondur.

| Syntax                 |
|------------------------|
| `TRUNC(tarih, format)` |

- `tarih` parametresi, belirtilen formata göre indirgenecek tarih verisidir.
- `format` parametresi, tarih/saat değerinin hangi formata/düzeye kadar indirgeneceğini belirtir. Eğer bu parametre belirtilmezse, değeri varsayılan olarak `DD` olur.

---

Aşağıdaki tabloda bu fonksiyon için kullanılabilecek formatlar ve açıklamaları yer almaktadır.

| Format                                             | Açıklama                                                                                                |
|----------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| `SYYYY`, `YYYY`, `SYEAR`, `YEAR`, `YYY`, `YY`, `Y` | Tarihin yılın ilk gününe indirgenmesini sağlar.                                                         |
| `Q`                                                | Tarihin bulunduğu çeyreğin ilk gününe indirgenmesini sağlar.                                            |
| `MONTH`, `MON`, `MM`, `RM`                         | Tarihin bulunduğu ayın ilk gününe indirgenmesini sağlar.                                                |
| `IW`                                               | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar.	ISO haftasının ilk günü Pazartesi'dir.     |
| `WW`                                               | x                                                                                                       |
| `W`                                                | x                                                                                                       |
| `DDD`, `DD`, `J`                                   | Tarihin saat bilgisinin sıfırlanmasını sağlar.                                                          |
| `DAY`, `DY`, `D`                                   | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar.                                            |
| `HH`, `HH12`, `HH24`                               | Tarihin saat bilgisinin saat başına indirgenmesini sağlar. Yani, dakika ve saniye bilgileri sıfırlanır. |
| `MI`                                               | Tarihin saat bilgisinin dakika başına indirgenmesini sağlar. Yani, saniye bilgisi sıfırlanır.           |

---

Aşağıdaki tabloda `TRUNC(datetime)` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım                                                                  | Sonuç               |
|---------------------------------------------------------------------------|---------------------|
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'SYYYY')` | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'YYYY')`  | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'SYEAR')` | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'YEAR')`  | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'YYY')`   | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'YY')`    | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'Y')`     | 01.01.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'Q')`     | 01.04.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MONTH')` | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MON')`   | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MM')`    | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'RM')`    | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'IW')`    | 19.05.2025 00:00:00 |
