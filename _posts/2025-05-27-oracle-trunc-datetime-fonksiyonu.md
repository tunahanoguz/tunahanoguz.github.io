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
| `SYYYY`, `YYYY`, `YEAR`, `SYEAR`, `YYY`, `YY`, `Y` | Tarihin yılın ilk gününe indirgenmesini sağlar.                                                         |
| `Q`                                                | Tarihin bulunduğu çeyreğin ilk gününe indirgenmesini sağlar.                                            |
| `MONTH`, `MON`, `MM`, `RM`                         | Tarihin bulunduğu ayın ilk gününe indirgenmesini sağlar.                                                |
| `HH`, `HH12`, `HH24`                               | Tarihin saat bilgisinin saat başına indirgenmesini sağlar. Yani, dakika ve saniye bilgileri sıfırlanır. |
| `MI`                                               | Tarihin saat bilgisinin dakika başına indirgenmesini sağlar. Yani, saniye bilgisi sıfırlanır.           |

---

Aşağıdaki tabloda `TRUNC(datetime)` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |
