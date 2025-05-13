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
3. [INTERVAL DAY TO SECOND](#interval-day-to-second)
    1. [NUMTODSINTERVAL Fonksiyonu](#numtodsinterval)
    2. [TO_DSINTERVAL Fonksiyonu](#to_dsinterval)

---

## 1. INTERVAL YEAR TO MONTH {#interval-year-to-month}

Yıl ve ay bazında zaman aralığı belirtir.

| Syntax                                                 | Açıklama                           |
|--------------------------------------------------------|------------------------------------|
| `INTERVAL YEAR[(yil_hassasiyeti)] TO MONTH`            | Veri tipini belirtir.              |
| `INTERVAL 'YIL[-AY]' YEAR[(yil_hassasiyeti)] TO MONTH` | Yıl ve ay bazlı aralık ifade eder. |
| `INTERVAL 'YIL' YEAR[(yil_hassasiyeti)]`               | Yıl bazlı aralık ifade eder.       |
| `INTERVAL 'AY' MONTH[(ay_hassasiyeti)]`                | Ay bazlı aralık ifade eder.        |

- `yil_hassasiyeti`, `YEAR` alanının alacağı sayının maksimum kaç haneden oluşabileceğini ifade eder. 0-9 arasında bir sayıyı kabul eder. Varsayılan değeri 2'dir. Varsayılan değerle birlikte en fazla 99 yıl 11 aylık bir aralığı ifade edilebilir. YEAR alanının alabileceği en büyük sayı 999.999.999'dur.
- `MONTH` alanı için hassasiyet belirtilmez. `YEAR TO MONTH` formatında kullanıldığında en az 0, en fazla 11 olabilir. Sadece `MONTH` formatında kullanıldığında en az 0, en fazla 12 olabilir.

| Kullanım                                    | Açıklama                                                                                                                 |
|---------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `INTERVAL '10-11' YEAR TO MONTH`            | 10 yıl 11 aylık aralık ifade eder.                                                                                       |
| `INTERVAL '120-11' YEAR(3) TO MONTH`        | 120 yıl 11 aylık aralık ifade eder. Yıl değeri 2'den fazla hane içerdiği için mutlaka `yil_hassasiyeti` belirtilmelidir. |
| `INTERVAL '10' YEAR`                        | 10 yıllık aralık ifade eder.                                                                                             |
| `INTERVAL '100' YEAR(3)`                    | 100 yıllık aralık ifade eder. Yıl değeri 2'den fazla hane içerdiği için mutlaka `yil_hassasiyeti` belirtilmelidir.       |
| `INTERVAL 'AY' MONTH`                       | AY aylık aralık ifade eder.                                                                                              |

### 1.1 NUMTOYMINTERVAL Fonksiyonu {#numtoyminterval}

### 1.2 TO_DSINTERVAL Fonksiyonu {#to_dsinterval}

---

## 2. INTERVAL DAY TO SECOND {#interval-day-to-second}

Gün, saat, dakika ve saniye bazında zaman aralığını belirtir.

| Syntax                                                                                      | Açıklama                                                    |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| `INTERVAL DAY[(GÜN_HASSASİYETİ)] TO SECOND[(KESİRLİ_SANİYE_HASSASİYETİ)]`                   | Veri tipini belirtir.                                       |
| `INTERVAL 'GÜN SAAT:DAKİKA:SANİYE.KESİRLİ_SANİYE' DAY TO SECOND[(YIL_HASSASİYETİ)]`         | Gün, saat, dakika ve saniye bazlı tarih aralığı ifade eder. |
| `INTERVAL 'GÜN SAAT:DAKİKA' DAY[(GÜN_HASSASİYETİ)] TO MINUTE`                               | Gün, saat ve dakika bazlı tarih aralığı ifade eder.         |
| `INTERVAL 'GÜN SAAT' DAY[(GÜN_HASSASİYETİ)] TO HOUR[(SAAT_HASSASİYETİ)]`                    | Gün ve saat bazlı tarih aralığı ifade eder.                 |
| `INTERVAL 'GÜN' DAY[(GÜN_HASSASİYETİ)]`                                                     | Gün bazlı tarih aralığı ifade eder.                         |
| `INTERVAL 'SAAT:DAKİKA:SANİYE.KESİRLİ_SANİYE' HOUR TO SECOND[(KESİRLİ_SANİYE_HASSASİYETİ)]` | Saat, dakika ve saniye bazlı tarih aralığı ifade eder.      |
| `INTERVAL 'SAAT:DAKİKA' HOUR TO MINUTE`                                                     | Saat ve dakika bazlı tarih aralığı ifade eder.              |
| `INTERVAL 'SAAT' HOUR`                                                                      | Saat bazlı tarih aralığı ifade eder.                        |
| `INTERVAL 'DAKİKA:SANİYE' MINUTE TO SECOND[(SAAT_HASSASİYETİ)]`                             | Dakika ve saniye bazlı tarih aralığı ifade eder.            |
| `INTERVAL 'DAKİKA' MINUTE`                                                                  | Dakika bazlı tarih aralığı ifade eder.                      |
| `INTERVAL 'SANİYE.KESİRLİ_SANİYE' SECOND(2,3)`                                              | Saniye bazlı tarih aralığı ifade eder.                      |

### 2.1 NUMTODSINTERVAL Fonksiyonu {#numtodsinterval}

### 2.2 TO_DSINTERVAL Fonksiyonu {#to_dsinterval}
