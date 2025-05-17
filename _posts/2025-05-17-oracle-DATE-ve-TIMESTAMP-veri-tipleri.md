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
3. [TIMESTAMP WITH TIME ZONE](#TIMESTAMP_WITH_TIME_ZONE)
  1. [SYSTIMESTAMP](#SYSTIMESTAMP)
  2. [CURRENT_TIMESTAMP](#CURRENT_TIMESTAMP)
4. [TIMESTAMP WITH LOCAL TIME ZONE](#TIMESTAMP_WITH_LOCAL_TIME_ZONE)
  1. [LOCALTIMESTAMP](#LOCALTIMESTAMP)

---

## 1. DATE {#date}

- Gün, ay, yıl, saat, dakika ve saniye bilgisi içeren tarihsel bir veri tipidir.
- Saniyenin kesirli kısmını içermez.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |

---

## 2. TIMESTAMP {#timestamp}

- DATE veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |

---

## 3. TIMESTAMP WITH TIME ZONE {#timestamp-with-time-zone}

- TIMESTAMP veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içerir.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |

---

## 4. TIMESTAMP WITH LOCAL TIME ZONE {#timestamp-with-local-time-zone}

- TIMESTAMP WITH TIME ZONE ile tek farkı zaman diliminin fiziksel olarak saklanmamasıdır.
- Veri sorgulandığında, kullanıcının zaman dilimi TIMESTAMP değerine iliştirilir.

| İlgili Fonksiyon | Açıklama |
|------------------|----------|
| x                | x        |
