---
title:  "Oracle - TRUNC(datetime) Fonksiyonu"
date: 2025-05-27 20:30:00 +0300
layout: post
categories: oracle
---

- `TRUNC(datetime)` fonksiyonu, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir verinin belirtilen birim düzeyine kadar indirgenmesini sağlar.
- Örnek olarak, değeri yılın ilk gününe, ayın ilk gününe veya haftanın ilk gününe indirger.
- Zamanın belirli bir formatına odaklanmak için kullanışlı bir fonksiyondur.
- Bu fonksiyonun dönüşü her zaman `DATE` tipindedir.

| Syntax                 |
|------------------------|
| `TRUNC(tarih, format)` |

- `tarih` parametresi, belirtilen formata göre indirgenecek tarih verisidir.
- `format` parametresi, tarih/saat değerinin hangi formata/düzeye kadar indirgeneceğini belirtir. Eğer bu parametre belirtilmezse, değeri varsayılan olarak `DD` olur.

---

Aşağıdaki tabloda bu fonksiyon için kullanılabilecek formatlar ve açıklamaları yer almaktadır.

| Format                                                         | Açıklama                                                                                                |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| `SYYYY`<br>`YYYY`<br>`SYEAR`<br>`YEAR`<br>`YYY`<br>`YY`<br>`Y` | Tarihin yılın ilk gününe indirgenmesini sağlar.                                                         |
| `IYYY`<br>`IY`<br>`I`                                          | Tarihin yılın ilk gününe indirgenmesini sağlar. Ancak bu formatın ifade ettiği yıl, ISO 8601 standartına göre olan yıldır. ISO 8601 standartına göre, standart yılın ilk Perşembe gününü içeren ve en az 4 günü standart yılın içerisinde yer alan hafta, ISO yılının ilk haftasıdır. ISO yılının ilk haftasının ilk günü ise yılın ilk günüdür. Bu sebeple, standart bir yılın takvimi ISO 8601 standartına göre belirlen yılın takvimi ile uyuşmayabilir. Örneğin, 2025 yılının ilk Perşembe günü 02.05.2025'tir ve bu günün bulunduğu haftanın 5 günü (01.01, 02.01, 03.01, 04.01, 05.01) standart yılın içinde yer almaktadır. Dolayısıyla bu hafta ISO yılının ilk haftası olarak kabul edilebilir. Böylece, haftanın ilk günü olan Pazartesi gününün ve ISO yılının ilk gününün tarihi 30.12.2024 olur.                                                     |
| `Q`                                                            | Tarihin bulunduğu çeyreğin ilk gününe indirgenmesini sağlar.                                            |
| `MONTH`<br>`MON`<br>`MM`<br>`RM`                               | Tarihin bulunduğu ayın ilk gününe indirgenmesini sağlar.                                                |
| `IW`                                                           | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar.	ISO haftasının ilk günü Pazartesi'dir.     |
| `WW`                                                           | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar. ISO haftasından farkı, haftanın ilk gününün, yılın ilk gününe denk gelen gün olarak kabul edilmesidir. Örneğin, 01.01.2025 Çarşamba günüdür, bu sebeple 19.05.2025 Pazartesi tarihinin haftanın ilk gününe indirgenmiş hali 14.05.2025 Çarşamba olur.                                                                                                                                                                      |
| `W`                                                            | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar. ISO haftasından farkı, haftanın ilk gününün, ayın ilk gününe denk gelen gün olarak kabul edilmesidir. Örneğin, 01.05.2025 Perşembe günüdür, bu sebeple 19.05.2025 Pazartesi tarihinin haftanın ilk gününe indirgenmiş hali 15.05.2025 Perşembe olur. |
| `DDD`<br>`DD`<br>`J`                                           | Tarihin saat bilgisinin sıfırlanmasını sağlar.                                                          |
| `DAY`<br>`DY`<br>`D`                                           | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar. Haftanın ilk günü, `NLS_TERRITORY` değerine göre değişebilir.                                                                                                                                                               |
| `HH`<br>`HH12`<br>`HH24`                                       | Tarihin saat bilgisinin saat başına indirgenmesini sağlar. Yani, dakika ve saniye bilgileri sıfırlanır. |
| `MI`                                                           | Tarihin saat bilgisinin dakika başına indirgenmesini sağlar. Yani, saniye bilgisi sıfırlanır.           |

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
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'IYYY')`  | 30.12.2024 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'IY')`    | 30.12.2024 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'I')`     | 30.12.2024 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'Q')`     | 01.04.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MONTH')` | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MON')`   | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MM')`    | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'RM')`    | 01.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'IW')`    | 19.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'WW')`    | 14.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'W')`     | 15.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DDD')`   | 19.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DD')`    | 19.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'J')`     | 19.05.2025 00:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DAY')`   | 18.05.2025 00:00:00 (`NLS_TERRITORY` => AMERICA) |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DY')`    | 18.05.2025 00:00:00 (`NLS_TERRITORY` => AMERICA) |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'D')`     | 18.05.2025 00:00:00 (`NLS_TERRITORY` => AMERICA) |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DAY')`   | 19.05.2025 00:00:00 (`NLS_TERRITORY` => TURKEY)  |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'DY')`    | 19.05.2025 00:00:00 (`NLS_TERRITORY` => TURKEY)  |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'D')`     | 19.05.2025 00:00:00 (`NLS_TERRITORY` => TURKEY)  |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'HH')`    | 19.05.2025 16:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'HH12')`  | 19.05.2025 16:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'HH24')`  | 19.05.2025 16:00:00 |
| `TRUNC(TO_DATE('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'), 'MI')`    | 19.05.2025 16:37:00 |
