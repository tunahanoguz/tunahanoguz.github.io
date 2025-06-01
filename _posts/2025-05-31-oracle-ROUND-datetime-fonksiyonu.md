---
title:  "Oracle - ROUND(datetime) Fonksiyonu"
date: 2025-05-31 17:15:00 +0300
layout: post
categories: oracle
---

- `ROUND(datetime)` fonksiyonu, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir verinin belirtilen tarih/saat birimine göre yuvarlar ve döner.
- Dönüş değeri `DATE` tipindedir.

| Syntax                    |
|---------------------------|
| `ROUND(tarih [, format])` |

- `tarih` parametresi, `DATE`, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipinde bir tarih değeridir.
- `format` parametresi, tarih değerinin hangi tarih/saat birimine göre yuvarlanacağını belirtir.

Aşağıdaki tabloda `ROUND(datetime)` fonksiyonu için kullanılabilecek formatlar ve açıklamaları yer almaktadır.

| Format                                                         | Açıklama                                                                                                |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| `SYYYY`<br>`YYYY`<br>`SYEAR`<br>`YEAR`<br>`YYY`<br>`YY`<br>`Y` | Tarih, 1 Temmuz'dan önceyse bulunduğu yılın başına, değilse sonraki yılın başına yuvarlanır.            |
| `IYYY`<br>`IY`<br>`I`                                          | Tarihin yılın ilk gününe indirgenmesini sağlar. Ancak bu formatın ifade ettiği yıl, ISO 8601 standartına göre olan yıldır. ISO 8601 standartına göre, standart yılın ilk Perşembe gününü içeren ve en az 4 günü standart yılın içerisinde yer alan hafta, ISO yılının ilk haftasıdır. ISO yılının ilk haftasının ilk günü ise yılın ilk günüdür. Bu sebeple, standart bir yılın takvimi ISO 8601 standartına göre belirlen yılın takvimi ile uyuşmayabilir. Örneğin, 2025 yılının ilk Perşembe günü 02.05.2025'tir ve bu günün bulunduğu haftanın 5 günü (01.01, 02.01, 03.01, 04.01, 05.01) standart yılın içinde yer almaktadır. Dolayısıyla bu hafta ISO yılının ilk haftası olarak kabul edilebilir. Böylece, haftanın ilk günü olan Pazartesi gününün ve ISO yılının ilk gününün tarihi 30.12.2024 olur.                                                     |
| `Q`                                                            | Tarih, bulunduğu çeyreğin ikinci ayının 16'sından önceyse bulunduğu çeyreğin başına, değilse bir sonraki çeyreğin başına yuvarlanır.                                                                                                                                                                |
| `MONTH`<br>`MON`<br>`MM`<br>`RM`                               | Tarih, bulunduğu ayın 16'sından önceyse bulunduğu ayın başına, değilse sonraki ayın başına yuvarlanır.  |
| `IW`                                                           | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar.	ISO haftasının ilk günü Pazartesi'dir.     |
| `WW`                                                           | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar. ISO haftasından farkı, haftanın ilk gününün, yılın ilk gününe denk gelen gün olarak kabul edilmesidir. Örneğin, 01.01.2025 Çarşamba günüdür, bu sebeple 19.05.2025 Pazartesi tarihinin haftanın ilk gününe indirgenmiş hali 14.05.2025 Çarşamba olur.                                                                                                                                                                      |
| `W`                                                            | Tarihin bulunduğu haftanın ilk gününe indirgenmesini sağlar. ISO haftasından farkı, haftanın ilk gününün, ayın ilk gününe denk gelen gün olarak kabul edilmesidir. Örneğin, 01.05.2025 Perşembe günüdür, bu sebeple 19.05.2025 Pazartesi tarihinin haftanın ilk gününe indirgenmiş hali 15.05.2025 Perşembe olur. |
| `DDD`<br>`DD`<br>`J`                                           | Tarih, öğlen 12'den önceyse bulunduğu günün başına, değilse sonraki günün başına yuvarlanır.            |
| `DAY`<br>`DY`<br>`D`                                           | Tarih, bulunduğu haftanın 5. gününden önceyse o haftanın ilk gününe, değilse sonraki haftanın ilk gününe yuvarlanır. Haftanın ilk günü, `NLS_TERRITORY` değerine göre değişebilir.                                                                                                              |
| `HH`<br>`HH12`<br>`HH24`                                       | Tarihin saat/dakika bilgisi, 30:00 öncesiyse içinde bulunulan saatin başına, değilse sonraki saatin başına yuvarlanır. |
| `MI`                                                           | Tarihin dakika bilgisi, 30'dan küçükse içinde bulunulan dakikanın başına, değilse sonraki dakikanın başına yuvarlanır. |

---

- Aşağıdaki tabloda `ROUND(datetime)` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH24:MI:SS` olarak belirlenmiştir.

| Kullanım                                              | Sonuç               |
|-------------------------------------------------------|---------------------|
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'SYYYY')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'SYYYY')` | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YYYY')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YYYY')`  | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'SYEAR')` | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'SYEAR')` | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YEAR')`  | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YEAR')`  | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YYY')`   | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YYY')`   | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'YY')`    | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'YY')`    | 01.01.2026 00:00:00 |
| `ROUND(TO_DATE('30.06.2025', 'DD.MM.YYYY'), 'Y')`     | 01.01.2025 00:00:00 |
| `ROUND(TO_DATE('01.07.2025', 'DD.MM.YYYY'), 'Y')`     | 01.01.2026 00:00:00 |
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
| `ROUND(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('20.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('21.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('22.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 19.05.2025 00:00:00 |
| `ROUND(TO_DATE('23.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 26.05.2025 00:00:00 |
| `ROUND(TO_DATE('24.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 26.05.2025 00:00:00 |
| `ROUND(TO_DATE('25.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'Turkey'`) | 26.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 18.05.2025 00:00:00 |
| `ROUND(TO_DATE('20.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 18.05.2025 00:00:00 |
| `ROUND(TO_DATE('21.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 18.05.2025 00:00:00 |
| `ROUND(TO_DATE('22.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 25.05.2025 00:00:00 |
| `ROUND(TO_DATE('23.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 25.05.2025 00:00:00 |
| `ROUND(TO_DATE('24.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 25.05.2025 00:00:00 |
| `ROUND(TO_DATE('25.05.2025', 'DD.MM.YYYY'), 'DAY')` (`NLS_TERRITORY = 'America'`) | 25.05.2025 00:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:29:59', 'DD.MM.YYYY HH24:MI:SS'), 'HH')`   | 19.05.2025 14:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:30:00', 'DD.MM.YYYY HH24:MI:SS'), 'HH')`   | 19.05.2025 15:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:29:59', 'DD.MM.YYYY HH24:MI:SS'), 'HH12')` | 19.05.2025 14:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:30:00', 'DD.MM.YYYY HH24:MI:SS'), 'HH12')` | 19.05.2025 15:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:29:59', 'DD.MM.YYYY HH24:MI:SS'), 'HH24')` | 19.05.2025 14:00:00 |
| `ROUND(TO_DATE('19.05.2025 14:30:00', 'DD.MM.YYYY HH24:MI:SS'), 'HH24')` | 19.05.2025 15:00:00 |
