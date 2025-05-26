---
title:  "Oracle - EXTRACT Fonksiyonu"
date: 2025-05-26 19:45:00 +0300
layout: post
categories: oracle
---

`EXTRACT` fonksiyonu, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir veriden bazı bilgilerin elde edilmesini sağlar.

Aşağıdaki tabloda bu bilgiler ve bu bilgilerin hangi tipteki verilerden elde edilebileceği yer almaktadır.

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

| Kullanım                                                                                         | Sonuç         |
|--------------------------------------------------------------------------------------------------|---------------|
| `EXTRACT(YEAR FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                         | 2025          |
| `EXTRACT(MONTH FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                        | 5             |
| `EXTRACT(DAY FROM TO_DATE('19.05.2025', 'DD.MM.YYYY'))`                                          | 19            |
| `EXTRACT(YEAR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`             | 2025          |
| `EXTRACT(MONTH FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`            | 5             |
| `EXTRACT(DAY FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`              | 19            |
| `EXTRACT(HOUR FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`             | 16            |
| `EXTRACT(MINUTE FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`           | 37            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48', 'DD.MM.YYYY HH24:MI:SS.FF'))`           | 49            |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.099999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.099999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.199999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.199999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.299999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.299999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.399999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.399999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.499999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.499999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.599999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.599999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.699999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.699999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.799999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.799999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.899999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.899999999  |
| `EXTRACT(SECOND FROM TO_TIMESTAMP('19.05.2025 16:37:48.999999999', 'DD.MM.YYYY HH24:MI:SS.FF'))` | 48.999999999  |
