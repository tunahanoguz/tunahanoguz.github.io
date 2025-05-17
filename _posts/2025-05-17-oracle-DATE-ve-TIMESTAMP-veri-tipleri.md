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

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| `SYSDATE`        | x        |
| `CURRENT_DATE`   | x        |
| `TO_DATE`        | x        |
| `TO_CHAR`        | x        |
| `EXTRACT`        | x        |
| `TRUNC`          | x        |
| `ROUND`          | x        |
| `ADD_MONTHS`     | x        |
| `MONTHS_BETWEEN` | x        |
| `LAST_DAY`       | x        |


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
