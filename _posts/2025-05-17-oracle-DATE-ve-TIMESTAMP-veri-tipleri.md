---
title:  "Oracle - DATE ve TIMESTAMP Veri Tipleri"
layout: post
categories: oracle
---

## İçindekiler
1. [DATE](#DATE)
2. [TIMESTAMP](#TIMESTAMP)
3. [TIMESTAMP WITH TIME ZONE](#TIMESTAMP-WITH-TIME-ZONE)
4. [TIMESTAMP WITH LOCAL TIME ZONE](#TIMESTAMP-WITH-LOCAL-TIME-ZONE)

---

## 1. DATE {#DATE}

- Gün, ay, yıl, saat, dakika ve saniye bilgisi içeren tarihsel bir veri tipidir.
- Saniyenin kesirli kısmını içermez.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00` olur.

---

## 2. TIMESTAMP {#TIMESTAMP}

- DATE veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

---

## 3. TIMESTAMP WITH TIME ZONE {#TIMESTAMP-WITH-TIME-ZONE}

- TIMESTAMP veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içerir.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

---

## 4. TIMESTAMP WITH LOCAL TIME ZONE {#TIMESTAMP-WITH-LOCAL-TIME-ZONE}

- TIMESTAMP WITH TIME ZONE ile tek farkı zaman diliminin fiziksel olarak saklanmamasıdır.
- Veri sorgulandığında, kullanıcının zaman dilimi TIMESTAMP değerine iliştirilir.
