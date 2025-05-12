---
title:  "Oracle - INTERVAL"
layout: post
categories: oracle
---

INTERVAL veri tipi, iki date time arasındaki zaman aralığını ifade eder ve detaylı zamansal hesaplamalar yapmamızı sağlar.

---

## İçindekiler
1. [INTERVAL YEAR TO MONTH](#interval-year-to-month)
    1. [NUMTOYMINTERVAL Fonksiyonu](#numtoyminterval)
    2. [TO_DSINTERVAL Fonksiyonu](#to_dsinterval)
    3. [Örnekler](#interval-year-to-month-ornekler)
3. [INTERVAL DAY TO SECOND](#interval-day-to-second)
    1. [NUMTODSINTERVAL Fonksiyonu](#numtodsinterval)
    2. [TO_DSINTERVAL Fonksiyonu](#to_dsinterval)
    3. [Örnekler](#interval-day-to-second-ornekler)

---

## 1. INTERVAL YEAR TO MONTH {#interval-year-to-month}

Yıl ve ay bazında zaman aralığını belirtir.

| Syntax                                                   |
|----------------------------------------------------------|
| INTERVAL YEAR [(yil_hassasiyeti)] TO MONTH               |
| INTERVAL 'year[-month]' YEAR[(yil_hassasiyeti)] TO MONTH |

- `yil_hassasiyeti`, YEAR alanının alacağı sayının maksimum kaç haneden oluşabileceğini ifade eder. 0-9 arasında bir sayıyı kabul eder. Varsayılan değeri 2'dir. Varsayılan değerle birlikte en fazla 99 yıl 11 aylık aralık ifade edilebilir. YEAR alanının alabileceği en büyük sayı 999.999.999'dur.

### 1.1 NUMTOYMINTERVAL Fonksiyonu {#numtoyminterval}

### 1.2 TO_DSINTERVAL Fonksiyonu {#to_dsinterval}

### 1.3 Örnekler {#interval-year-to-month-ornekler}

## 2. INTERVAL DAY TO SECOND {#interval-day-to-second}

Gün, saat, dakika ve saniye bazında zaman aralığını belirtir.

### 2.1 NUMTODSINTERVAL Fonksiyonu {#numtodsinterval}

### 2.2 TO_DSINTERVAL Fonksiyonu {#to_dsinterval}

### 2.3 Örnekler {#interval-day-to-second-ornekler}
