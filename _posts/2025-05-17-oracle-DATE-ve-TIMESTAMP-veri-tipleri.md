---
title:  "Oracle - DATE ve TIMESTAMP Veri Tipleri"
layout: post
categories: oracle
---

---

## İçindekiler
1. [DATE](#DATE)
    1. [SYSDATE](#SYSDATE)
    2. [CURRENT_DATE](#CURRENT_DATE)
    3. [TO_DATE](#TO_DATE)
2. [TIMESTAMP](#TIMESTAMP)
3. [TIMESTAMP WITH TIME ZONE](#TIMESTAMP-WITH-TIME-ZONE)
    1. [SYSTIMESTAMP](#SYSTIMESTAMP)
    2. [CURRENT_TIMESTAMP](#CURRENT_TIMESTAMP)
4. [TIMESTAMP WITH LOCAL TIME ZONE](#TIMESTAMP-WITH-LOCAL-TIME-ZONE)
    1. [LOCALTIMESTAMP](#LOCALTIMESTAMP)

---

## 1. DATE {#DATE}

- Gün, ay, yıl, saat, dakika ve saniye bilgisi içeren tarihsel bir veri tipidir.
- Saniyenin kesirli kısmını içermez.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00` olur.

| İlgili Fonksiyon | Açıklama                                                                                             |
|------------------|------------------------------------------------------------------------------------------------------|
| [`SYSDATE` 🔗](#DATE)        | Sistemin tarih ve saat bilgisini DATE tipinde verir.                                                 |
| `CURRENT_DATE`   | Kullanıcı oturumunda ayarlanmış time zone bilgisine göre DATE tipinde tarih ve saat bilgisini verir. |
| `TO_DATE`        | Bir string'i DATE veri tipine çevirir.                                                               |
| `TO_CHAR`        | DATE tipindeki bir değeri string'e çevirir.                                                          |
| `EXTRACT`        | Gün, ay, yıl, saat, dakika ve saniye bilgisini numerik bir değeri olarak verir.                      |
| `TRUNC`          | Bir tarihi gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında aşağıya yuvarlar.                     |
| `ROUND`          | Bir tarihi gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında yuvarlar.                             |
| `ADD_MONTHS`     | Bir tarihe belirtilen sayı kadar ay ekler.                                                           |
| `MONTHS_BETWEEN` | İki tarih arasındaki ay farkını verir.                                                               |
| `LAST_DAY`       | Verilen tarihteki ay için ayın son gününü verir.                                                     |

- Aşağıdaki tabloda yukarıda açıklamaları verilen fonksiyonlar için örnekler bulunmaktadır.
- Session tarih formatı `DD.MM.YYYY HH24:MI:SS` olarak ayarlanmıştır.
- Sorgular 2025 yılının mayıs ayında çalıştırılmıştır.

| Kullanım                                                  | Sonuç               |
|-----------------------------------------------------------|---------------------|
| `TO_DATE('17.05.2025', 'DD.MM.YYYY')`                     | 17.05.2025 00:00:00 |
| `TO_DATE('17.05.2025 14:37:28', 'DD.MM.YYYY HH24:MI:SS')` | 17.05.2025 14:37:28 |
| `TO_DATE('17', 'DD')`                                     | 17.05.2025 00:00:00 |
| `TO_DATE('05', 'MM')`                                     | 01.05.2025 00:00:00 |
| `TO_DATE('2025', 'YYYY')`                                 | 01.01.2025 00:00:00 |
| `TO_DATE('14', 'HH24')`                                   | 01.05.2025 14:00:00 |
| `TO_DATE('37', 'MI')`                                     | 01.05.2025 00:37:00 |
| `TO_DATE('28', 'SS')`                                     | 01.05.2025 00:00:28 |
| `TO_DATE('17.05', 'DD.MM')`                               | 17.05.2025 00:00:00 |
| `TO_DATE('05.2025', 'MM.YYYY')`                           | 01.05.2025 00:00:00 |
| `TO_DATE('17.2025', 'DD.YYYY')`                           | 17.05.2025 00:00:00 |
| `TO_DATE('14:37', 'HH24:MI')`                             | 01.05.2025 14:37:00 |
| `TO_DATE('14:37:28', 'HH24:MI:SS')`                       | 01.05.2025 14:37:28 |
| `TO_DATE('1', 'DDD')`                                     | 01.01.2025 00:00:00 |
| `TO_DATE('2', 'DDD')`                                     | 02.01.2025 00:00:00 |
| `TO_DATE('364', 'DDD')`                                   | 30.12.2025 00:00:00 |
| `TO_DATE('365', 'DDD')`                                   | 31.01.2025 00:00:00 |
| `TO_DATE('MAY', 'MON')`                                   | 01.05.2025 00:00:00 |

---

## 2. TIMESTAMP {#TIMESTAMP}

- DATE veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| `TO_TIMESTAMP`   | x        |
| `TO_CHAR`        | x        |
| `EXTRACT`        | x        |
| `TRUNC`          | x        |
| `ROUND`          | x        |
| `ADD_MONTHS`     | x        |
| `MONTHS_BETWEEN` | x        |
| `LAST_DAY`       | x        |

---

## 3. TIMESTAMP WITH TIME ZONE {#TIMESTAMP-WITH-TIME-ZONE}

- TIMESTAMP veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içerir.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon    | Açıklama                                                                                                                                      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `SYSTIMESTAMP`      | Sistemin tarih ve saat bilgisini `TIMESTAMP WITH TIME ZONE` tipinde verir.                                                                    |
| `CURRENT_TIMESTAMP` | Kullanıcı oturumunda ayarlanmış time zone bilgisine göre `TIMESTAMP WITH TIME ZONE` tipinde tarih ve saat bilgisini verir.                    |
| `TO_TIMESTAMP_TZ`   | Bir string'i `TIMESTAMP WITH TIME ZONE` tipine çevirir.                                                                                       |
| `FROM_TZ`           | `TIMESTAMP` tipinde bir değeri `TIMESTAMP WITH TIME ZONE` tipine çevirir.                                                                     |
| `TO_CHAR`           | `TIMESTAMP WITH TIME ZONE` tipindeki bir değeri string'e çevirir.                                                                             |
| `EXTRACT`           | Gün, ay, yıl, saat, dakika, saniye, saniyenin kesirli kısmı ve zaman dilimi bilgisini numerik bir değeri olarak verir.                        |
| `TRUNC`             | `TIMESTAMP WITH TIME ZONE` tipindeki bir değeri gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında aşağıya yuvarlar ve `DATE` tipinde döner. |
| `ROUND`             | `TIMESTAMP WITH TIME ZONE` tipindeki bir değeri gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında yuvarlar ve `DATE` tipinde döner.         |
| `ADD_MONTHS`        | `TIMESTAMP WITH TIME ZONE` tipindeki bir değere belirtilen sayı kadar ay ekler ve `DATE` tipinde döner.                                       |
| `MONTHS_BETWEEN`    | `TIMESTAMP WITH TIME ZONE` tipindeki iki değer arasındaki ay farkını verir.                                                                   |
| `LAST_DAY`          | `TIMESTAMP WITH TIME ZONE` tipindeki bir değerdeki ay için ayın son gününü verir ve `DATE` tipinde döner.                                     |

---

## 4. TIMESTAMP WITH LOCAL TIME ZONE {#TIMESTAMP-WITH-LOCAL-TIME-ZONE}

- TIMESTAMP WITH TIME ZONE ile tek farkı zaman diliminin fiziksel olarak saklanmamasıdır.
- Veri sorgulandığında, kullanıcının zaman dilimi TIMESTAMP değerine iliştirilir.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |
