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

| Syntax                                            | Açıklama                           |
|---------------------------------------------------|------------------------------------|
| `INTERVAL YEAR[(hassasiyet)] TO MONTH`            | Veri tipi gösterimidir.            |
| `INTERVAL 'YIL[-AY]' YEAR[(hassasiyet)] TO MONTH` | Yıl ve ay bazlı aralık ifade eder. |
| `INTERVAL 'YIL' YEAR[(hassasiyet)]`               | Yıl bazlı aralık ifade eder.       |
| `INTERVAL 'AY' MONTH`                             | Ay bazlı aralık ifade eder.        |

- Yıl hassasiyeti;
    - 0 ve 9 arasında olabilir.
    - Varsayılan değeri 2'dir.
    - 0 olduğunda yıl değeri için 0 basamaklık yer ayrılır. Yani yıl değeri tutulmaz, yalnızca ay değeri tutulur.
- Ay hassasiyeti;
    - Yıl ve ay bazlı aralık ifade edilirken 2 ile sınırlandırılır. Bu durumda ay değeri en az 0 en fazla 11 olabilir.
    - Tek başına ay bazlı aralık ifade edildiği durumda sınırsızdır. -11'den küçük veya 11'den büyük değerler için 12'den büyük kısmı yıla dahil edilerek ay-yıl hesabı otomatik bir şekilde yapılır.

| Kullanım                                    | Açıklama                            | Sonuç   |
|---------------------------------------------|-------------------------------------|---------|
| `INTERVAL '0-0' YEAR TO MONTH`              | 0 yıl 0 aylık aralık ifade eder.    | +0-0    |
| `INTERVAL '0-1' YEAR TO MONTH`              | 0 yıl 1 aylık aralık ifade eder.    | +0-1    |
| `INTERVAL '1-0' YEAR TO MONTH`              | 1 yıl 0 aylık aralık ifade eder.    | +1-0    |
| `INTERVAL '10-1' YEAR TO MONTH`             | 10 yıl 1 aylık aralık ifade eder.   | +10-1   |
| `INTERVAL '99-11' YEAR TO MONTH`            | 99 yıl 11 aylık aralık ifade eder.  | +99-11  |
| `INTERVAL '100-1' YEAR(3) TO MONTH`         | 100 yıl 1 aylık aralık ifade eder.  | +100-1  |
| `INTERVAL '999-11' YEAR(3) TO MONTH`        | 999 yıl 11 aylık aralık ifade eder. | +999-11 |
| `INTERVAL '0' YEAR`                         | 0 yıllık aralık ifade eder.         | +0-0    |
| `INTERVAL '1' YEAR`                         | 1 yıllık aralık ifade eder.         | +1-0    |
| `INTERVAL '10' YEAR`                        | 10 yıllık aralık ifade eder.        | +10-0   |
| `INTERVAL '99' YEAR`                        | 99 yıllık aralık ifade eder.        | +99-0   |
| `INTERVAL '0' YEAR(3)`                      | 0 yıllık aralık ifade eder.         | +0-0    |
| `INTERVAL '1' YEAR(3)`                      | 1 yıllık aralık ifade eder.         | +1-0    |
| `INTERVAL '10' YEAR(3)`                     | 10 yıllık aralık ifade eder.        | +10-0   |
| `INTERVAL '99' YEAR(3)`                     | 99 yıllık aralık ifade eder.        | +99-0   |
| `INTERVAL '100' YEAR(3)`                    | 100 yıllık aralık ifade eder.       | +100-0  |
| `INTERVAL '999' YEAR(3)`                    | 999 yıllık aralık ifade eder.       | +999-0  |
| `INTERVAL '0' MONTH`                        | 0 aylık aralık ifade eder.          | +0-0    |
| `INTERVAL '1' MONTH`                        | 1 aylık aralık ifade eder.          | +0-1    |
| `INTERVAL '11' MONTH`                       | 11 aylık aralık ifade eder.         | +0-11   |
| `INTERVAL '12' MONTH`                       | 12 aylık aralık ifade eder.         | +1-0    |
| `INTERVAL '23' MONTH`                       | 23 aylık aralık ifade eder.         | +1-11   |
| `INTERVAL '24' MONTH`                       | 24 aylık aralık ifade eder.         | +2-0    |

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
