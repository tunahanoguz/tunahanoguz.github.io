---
title:  "Oracle - EXTRACT Fonksiyonu"
date: 2025-05-26 19:45:00 +0300
layout: post
categories: oracle
---

`EXTRACT` fonksiyonu, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir veriden belirli bir tarih/saat bileşeninin elde edilmesini sağlar.

Aşağıdaki tabloda bu bileşenler ve bu bileşenlerin hangi tipteki verilerden elde edilebileceği yer almaktadır.

| Bilgi             | DATE | TIMESTAMP | TIMESTAMP WITH TIME ZONE | INTERVAL YEAR TO MONTH | INTERVAL DAY TO SECOND |
|-------------------|------|-----------|--------------------------|------------------------|------------------------|
| `YEAR`            | 🟢   | 🟢        | 🟢                        | 🟢                     | 🔴                      |
| `MONTH`           | 🟢   | 🟢        | 🟢                        | 🟢                     | 🔴                      |
| `DAY`             | 🟢   | 🟢        | 🟢                        | 🔴                     | 🟢                      |
| `HOUR`            | 🔴   | 🟢        | 🟢                        | 🔴                     | 🟢                      |
| `MINUTE`          | 🔴   | 🟢        | 🟢                        | 🔴                     | 🟢                      |
| `SECOND`          | 🔴   | 🟢        | 🟢                        | 🔴                     | 🟢                      |
| `TIMEZONE_HOUR`   | 🔴   | 🔴        | 🟢                        | 🔴                     | 🔴                      |
| `TIMEZONE_MINUTE` | 🔴   | 🔴        | 🟢                        | 🔴                     | 🔴                      |
| `TIMEZONE_REGION` | 🔴   | 🔴        | 🟢                        | 🔴                     | 🔴                      |
| `TIMEZONE_ABBR`   | 🔴   | 🔴        | 🟢                        | 🔴                     | 🔴                      |

---

Aşağıdaki tabloda `EXTRACT` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım                                                                                                            | Sonuç         |
|---------------------------------------------------------------------------------------------------------------------|---------------|
| `EXTRACT(YEAR FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                                            | 2025          |
| `EXTRACT(MONTH FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                                           | 5             |
| `EXTRACT(DAY FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                                             | 19            |
| `EXTRACT(HOUR FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                                            | ORA-30076: invalid extract field for extract source |
| `EXTRACT(YEAR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                   | 2025          |
| `EXTRACT(MONTH FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                  | 5             |
| `EXTRACT(DAY FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                    | 19            |
| `EXTRACT(HOUR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                   | 16            |
| `EXTRACT(MINUTE FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                 | 37            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                                 | 48            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.099999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.099999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.199999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.199999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.299999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.299999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.399999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.399999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.499999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.499999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.599999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.599999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.699999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.699999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.799999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.799999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.899999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.899999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.999999999', 'DD.MM.YYYY HH24:MI:SS.FF'))`                    | 48.999999999  |
| `EXTRACT(TIMEZONE_HOUR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                          | ORA-30076: invalid extract field for extract source |
| `EXTRACT(TIMEZONE_MINUTE FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                        | ORA-30076: invalid extract field for extract source |
| `EXTRACT(TIMEZONE_REGION FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                        | ORA-30076: invalid extract field for extract source |
| `EXTRACT(TIMEZONE_ABBR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS'))`                          | ORA-30076: invalid extract field for extract source |
| `EXTRACT(YEAR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`                 | 2025          |
| `EXTRACT(MONTH FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`                | 5             |
| `EXTRACT(DAY FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`                  | 19            |
| `EXTRACT(HOUR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`                 | 16            |
| `EXTRACT(MINUTE FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`               | 37            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`               | 48            |
| `EXTRACT(TIMEZONE_HOUR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`        | 3             |
| `EXTRACT(TIMEZONE_MINUTE FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`      | 0             |
| `EXTRACT(TIMEZONE_REGION FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`      | UNKNOWN       |
| `EXTRACT(TIMEZONE_ABBR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 +03:00', 'DD.MM.YYYY HH24:MI:SS TZH:TZM'))`        | UNK           |
| `EXTRACT(YEAR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`            | 2025          |
| `EXTRACT(MONTH FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZHR'))`          | 5             |
| `EXTRACT(DAY FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`             | 19            |
| `EXTRACT(HOUR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`            | 16            |
| `EXTRACT(MINUTE FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`          | 37            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`          | 48            |
| `EXTRACT(TIMEZONE_HOUR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`   | 3             |
| `EXTRACT(TIMEZONE_MINUTE FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))` | 0             |
| `EXTRACT(TIMEZONE_REGION FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))` | Europe/Istanbul |
| `EXTRACT(TIMEZONE_ABBR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Istanbul', 'DD.MM.YYYY HH24:MI:SS TZR'))`   | +03           |
| `EXTRACT(TIMEZONE_REGION FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Paris', 'DD.MM.YYYY HH24:MI:SS TZR'))`    | Europe/Paris  |
| `EXTRACT(TIMEZONE_ABBR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Paris', 'DD.MM.YYYY HH24:MI:SS TZR'))`      | CEST          |
| `EXTRACT(TIMEZONE_REGION FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Lisbon', 'DD.MM.YYYY HH24:MI:SS TZR'))`   | Europe/Lisbon |
| `EXTRACT(TIMEZONE_ABBR FROM TO_TIMESTAMP_TZ('19.05.2025 16:37:48 Europe/Lisbon', 'DD.MM.YYYY HH24:MI:SS TZR'))`     | WEST          |
| `EXTRACT(YEAR FROM TO_YMINTERVAL('10-2'))`                                                                          | 10            |
| `EXTRACT(MONTH FROM TO_YMINTERVAL('10-2'))`                                                                         | 2             |
| `EXTRACT(DAY FROM TO_YMINTERVAL('10-2'))`                                                                           | ORA-30076: invalid extract field for extract source |
| `EXTRACT(YEAR FROM NUMTOYMINTERVAL(10, 'YEAR'))`                                                                    | 10            |
| `EXTRACT(MONTH FROM NUMTOYMINTERVAL(10, 'YEAR'))`                                                                   | 0             |
| `EXTRACT(DAY FROM NUMTOYMINTERVAL(10, 'YEAR'))`                                                                     | ORA-30076: invalid extract field for extract source |
| `EXTRACT(YEAR FROM NUMTOYMINTERVAL(10, 'MONTH'))`                                                                   | 0             |
| `EXTRACT(MONTH FROM NUMTOYMINTERVAL(10, 'MONTH'))`                                                                  | 10            |
| `EXTRACT(DAY FROM NUMTOYMINTERVAL(10, 'MONTH'))`                                                                    | ORA-30076: invalid extract field for extract source |
| `EXTRACT(HOUR FROM TO_DSINTERVAL('0 0:0:0.0'))`                                                                     | 0             |
| `EXTRACT(MINUTE FROM TO_DSINTERVAL('0 0:0:0.0'))`                                                                   | 0             |
| `EXTRACT(SECOND FROM TO_DSINTERVAL('0 0:0:0.0'))`                                                                   | 0             |
| `EXTRACT(HOUR FROM TO_DSINTERVAL('999999999 23:59:59.999999999'))`                                                  | 23            |
| `EXTRACT(MINUTE FROM TO_DSINTERVAL('999999999 23:59:59.999999999'))`                                                | 59            |
| `EXTRACT(SECOND FROM TO_DSINTERVAL('999999999 23:59:59.999999999'))`                                                | 59.999999999  |
| `EXTRACT(DAY FROM NUMTODSINTERVAL(10, 'DAY'))`                                                                      | 10            |
| `EXTRACT(HOUR FROM NUMTODSINTERVAL(10, 'DAY'))`                                                                     | 0             |
| `EXTRACT(MINUTE FROM NUMTODSINTERVAL(10, 'DAY'))`                                                                   | 0             |
| `EXTRACT(SECOND FROM NUMTODSINTERVAL(10, 'DAY'))`                                                                   | 0             |
| `EXTRACT(HOUR FROM NUMTODSINTERVAL(16, 'HOUR'))`                                                                    | 16            |
| `EXTRACT(DAY FROM NUMTODSINTERVAL(16, 'HOUR'))`                                                                     | 0             |
| `EXTRACT(MINUTE FROM NUMTODSINTERVAL(16, 'HOUR'))`                                                                  | 0             |
| `EXTRACT(SECOND FROM NUMTODSINTERVAL(16, 'HOUR'))`                                                                  | 0             |
| `EXTRACT(MINUTE FROM NUMTODSINTERVAL(37, 'MINUTE'))`                                                                | 37            |
| `EXTRACT(DAY FROM NUMTODSINTERVAL(37, 'MINUTE'))`                                                                   | 0             |
| `EXTRACT(HOUR FROM NUMTODSINTERVAL(37, 'MINUTE'))`                                                                  | 0             |
| `EXTRACT(SECOND FROM NUMTODSINTERVAL(37, 'MINUTE'))`                                                                | 0             |
| `EXTRACT(SECOND FROM NUMTODSINTERVAL(48, 'SECOND'))`                                                                | 48            |
| `EXTRACT(DAY FROM NUMTODSINTERVAL(48, 'SECOND'))`                                                                   | 0             |
| `EXTRACT(HOUR FROM NUMTODSINTERVAL(48, 'SECOND'))`                                                                  | 0             |
| `EXTRACT(MINUTE FROM NUMTODSINTERVAL(48, 'SECOND'))`                                                                | 0             |
