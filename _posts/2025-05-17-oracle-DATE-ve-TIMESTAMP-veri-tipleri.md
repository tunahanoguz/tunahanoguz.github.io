---
title:  "Oracle - DATE ve TIMESTAMP Veri Tipleri"
layout: post
categories: oracle
---

---

## İçindekiler
1. [DATE](#date)
2. [TIMESTAMP](#timestamp)
2. [TIMESTAMP WITH TIME ZONE](#timestamp-with-time-zone)
2. [TIMESTAMP WITH LOCAL TIME ZONE](#timestamp-with-local-time-zone)

---

## 1. DATE {#date}

- Gün, ay, yıl, saat, dakika ve saniye bilgisi içeren tarihsel bir veri tipidir.
- Saniyenin kesirli kısmını içermez.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00` olur.

---

## 2. TIMESTAMP {#timestamp}

- DATE veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içermez.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

---

## 3. TIMESTAMP WITH TIME ZONE {#timestamp-with-time-zone}

- TIMESTAMP veri tipinin daha hassas halidir.
- Saniyenin kesirli kısmını içerir.
- Zaman dilimi içerir.
- Belirtilmediği durumda varsayılan saat bilgisi `00:00:00.000000000` olur.

---

## 4. TIMESTAMP WITH LOCAL TIME ZONE {#timestamp-with-local-time-zone}

- TIMESTAMP WITH TIME ZONE ile tek farkı zaman diliminin fiziksel olarak saklanmamasıdır.
- Veri sorgulandığında, kullanıcının zaman dilimi TIMESTAMP değerine iliştirilir.
