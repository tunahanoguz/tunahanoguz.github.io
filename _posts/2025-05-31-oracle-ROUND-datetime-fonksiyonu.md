---
title:  "Oracle - ROUND(datetime) Fonksiyonu"
date: 2025-05-31 17:15:00 +0300
layout: post
categories: oracle
---

`ROUND(datetime)` fonksiyonu, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir verinin belirtilen tarih/saat birimine göre yuvarlar ve döner.

| Syntax                    |
|---------------------------|
| `ROUND(tarih [, format])` |

- `tarih` parametresi, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipinde bir tarih değeridir.
- `format` parametresi, tarih değerinin hangi tarih/saat birimine göre yuvarlanacağını belirtir.

Aşağıdaki tabloda `ROUND(datetime)` fonksiyonu için kullanılabilecek formatlar ve açıklamaları yer almaktadır.

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

Aşağıdaki tabloda `ROUND(datetime)` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım                                              | Sonuç               |
|-------------------------------------------------------|---------------------|
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'SYYYY')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'SYYYY')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YYYY')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YYYY')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'SYEAR')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'SYEAR')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YEAR')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YEAR')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YYY')`   | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YYY')`   | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YY')`    | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YY')`    | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'Y')`     | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'Y')`     | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('15.02.2025', 'DD.MM.YYYY'), 'Q')`     | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('16.02.2025', 'DD.MM.YYYY'), 'Q')`     | 01.04.2025 00:00:00 |
| `ROUND(TO_DATE('15.05.2025', 'DD.MM.YYYY'), 'Q')`     | 01.04.2025 00:00:00 |
| `ROUND(TO_DATE('16.05.2025', 'DD.MM.YYYY'), 'Q')`     | 01.07.2025 00:00:00 |
| `ROUND(TO_DATE('15.08.2025', 'DD.MM.YYYY'), 'Q')`     | 01.07.2025 00:00:00 |
| `ROUND(TO_DATE('16.08.2025', 'DD.MM.YYYY'), 'Q')`     | 01.10.2025 00:00:00 |
| `ROUND(TO_DATE('15.11.2025', 'DD.MM.YYYY'), 'Q')`     | 01.10.2025 00:00:00 |
| `ROUND(TO_DATE('16.11.2025', 'DD.MM.YYYY'), 'Q')`     | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('15.05.2025', 'DD.MM.YYYY'), 'MONTH')` | 01.05.2025 00:00:00 |
| `ROUND(TO_DATE('16.05.2025', 'DD.MM.YYYY'), 'MONTH')` | 01.06.2025 00:00:00 |
| `ROUND(TO_DATE('15.05.2025', 'DD.MM.YYYY'), 'MON')`   | 01.05.2025 00:00:00 |
| `ROUND(TO_DATE('16.05.2025', 'DD.MM.YYYY'), 'MON')`   | 01.06.2025 00:00:00 |
| `ROUND(TO_DATE('15.05.2025', 'DD.MM.YYYY'), 'MM')`    | 01.05.2025 00:00:00 |
| `ROUND(TO_DATE('16.05.2025', 'DD.MM.YYYY'), 'MM')`    | 01.06.2025 00:00:00 |
| `ROUND(TO_DATE('15.05.2025', 'DD.MM.YYYY'), 'RM')`    | 01.05.2025 00:00:00 |
| `ROUND(TO_DATE('16.05.2025', 'DD.MM.YYYY'), 'RM')`    | 01.06.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 11:59:59', 'DD.MM.YYYY HH24:MI:SS'), 'DDD')` | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 12:00:00', 'DD.MM.YYYY HH24:MI:SS'), 'DDD')` | 20.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 11:59:59', 'DD.MM.YYYY HH24:MI:SS'), 'DD')`  | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 12:00:00', 'DD.MM.YYYY HH24:MI:SS'), 'DD')`  | 20.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 11:59:59', 'DD.MM.YYYY HH24:MI:SS'), 'J')`   | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 12:00:00', 'DD.MM.YYYY HH24:MI:SS'), 'J')`   | 20.05.2025 00:00:00 |
