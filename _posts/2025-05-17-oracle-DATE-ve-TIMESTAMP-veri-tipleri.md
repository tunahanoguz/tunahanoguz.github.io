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
| `SYSDATE`        | Sistemin tarih ve saat bilgisini DATE tipinde verir.                                                 |
| `CURRENT_DATE`   | Kullanıcı oturumunda ayarlanmış time zone bilgisine göre DATE tipinde tarih ve saat bilgisini verir. |
| `TO_DATE`        | Bir string'i DATE veri tipine çevirir.                                                               |
| `TO_CHAR`        | DATE tipindeki bir değeri string'e çevirir.                                                          |
| `EXTRACT`        | Gün, ay, yıl, saat, dakika ve saniye bilgisini numerik bir değeri olarak verir.                      |
| `TRUNC`          | Bir tarihi gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında aşağıya yuvarlar.                     |
| `ROUND`          | Bir tarihi gün, ay, yıl, saat, dakika, çeyrek ve hafta bazında yuvarlar.                             |
| `ADD_MONTHS`     | Bir tarihe belirtilen sayı kadar ay ekler.                                                           |
| `MONTHS_BETWEEN` | İki tarih arasındaki ay farkını verir.                                                               |
| `LAST_DAY`       | Verilen tarihteki ay için ayın son gününü verir.                                                     |


---

## 2. TIMESTAMP {#TIMESTAMP}

- DATE veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |

---

## 3. TIMESTAMP WITH TIME ZONE {#TIMESTAMP-WITH-TIME-ZONE}

- TIMESTAMP veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içerir.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |

---

## 4. TIMESTAMP WITH LOCAL TIME ZONE {#TIMESTAMP-WITH-LOCAL-TIME-ZONE}

- TIMESTAMP WITH TIME ZONE ile tek farkı zaman diliminin fiziksel olarak saklanmamasıdır.
- Veri sorgulandığında, kullanıcının zaman dilimi TIMESTAMP değerine iliştirilir.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |
