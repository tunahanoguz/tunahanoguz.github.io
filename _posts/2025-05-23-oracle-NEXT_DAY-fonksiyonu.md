---
title:  "Oracle - NEXT_DAY Fonksiyonu"
date: 2025-05-23 22:15:00 +0300
layout: post
categories: oracle
---

`NEXT_DAY` fonksiyonu, bir tarih değerinden sonraki belirli bir hafta gününü `DATE` tipinde döner.

| Syntax                   |
|--------------------------|
| NEXT_DAY(tarih, gun_adi) |

- `tarih` parametresi, `DATE`, `TIMESTAMP` ve `TIMESTAMP WITH TIME ZONE` tipinde tarihsel bir değerdir.
- `gun_adi` parametresi, haftanın bir gününün adını ifade eder. `NLS_DATE_LANGUAGE` initialization parametresinin değerine göre isimler değişiklik gösterebilir.

---

- Aşağıdaki tabloda `NEXT_DAY` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS AM BC` olarak belirlenmiştir.
- Sorgular **19.05.2025** tarihinde çalıştırılmıştır.

| Kullanım                                                     | Sonuç                     |
|--------------------------------------------------------------|---------------------------|
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'MON')`       | 26.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'TUE')`       | 20.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'WED')`       | 21.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'THU')`       | 22.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'FRI')`       | 23.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SAT')`       | 24.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SUN')`       | 25.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'MONDAY')`    | 26.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'TUESDAY')`   | 20.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'WEDNESDAY')` | 21.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'THURSDAY')`  | 22.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'FRIDAY')`    | 23.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SATURDAY')`  | 24.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SUNDAY')`    | 25.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PZT')`       | 26.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SAL')`       | 20.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'ÇAR')`       | 21.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PER')`       | 22.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'CUM')`       | 23.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'CMT')`       | 24.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PAZ')`       | 25.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PAZARTESİ')` | 26.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'SALI')`      | 20.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'ÇARŞAMBA')`  | 21.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PERŞEMBE')`  | 22.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'CUMA')`      | 23.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'CUMARTESİ')` | 24.05.2025 12:00:00 AM AD |
| `NEXT_DAY(TO_DATE('19.05.2025', 'DD.MM.YYYY'), 'PAZAR')`     | 25.05.2025 12:00:00 AM AD |
