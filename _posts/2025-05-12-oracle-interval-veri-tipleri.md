---
title:  "Oracle - INTERVAL Veri Tipleri"
layout: post
categories: oracle
---

INTERVAL veri tipleri, bir süreyi/zaman aralığını ifade eder.

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

Bir sayıyı `INTERVAL YEAR TO MONTH` tipine çevirir.

| Syntax                                    |
|-------------------------------------------|
| ```NUMTOYMINTERVAL(sayi, MONTH | YEAR)``` |

Aşağıdaki tabloda NUMTOYMINTERVAL fonksiyonunun kullanım örnekleri bulunmaktadır.

| Kullanım                       | Sonuç         |
|--------------------------------|---------------|
| `NUMTOYMINTERVAL(0, 'MONTH')`  | +000000000-00 |
| `NUMTOYMINTERVAL(1, 'MONTH')`  | +000000000-01 |
| `NUMTOYMINTERVAL(11, 'MONTH')` | +000000000-11 |
| `NUMTOYMINTERVAL(12, 'MONTH')` | +000000001-00 |
| `NUMTOYMINTERVAL(0, 'YEAR')`   | +000000000-00 |
| `NUMTOYMINTERVAL(1, 'YEAR')`   | +000000001-00 |

### 1.2 TO_YMINTERVAL Fonksiyonu {#to_dsinterval}

Bir string'i `INTERVAL YEAR TO MONTH` tipine çevirir.

| Syntax                                    |
|-------------------------------------------|
| `TO_YMINTERVAL(string)`                   |

Aşağıdaki tabloda TO_YMINTERVAL fonksiyonunun kullanım örnekleri bulunmaktadır.

| Kullanım                         | Sonuç                                      |
|----------------------------------|--------------------------------------------|
| `TO_YMINTERVAL('0-0')`           | +000000000-00                              |
| `TO_YMINTERVAL('0-1')`           | +000000000-01                              |
| `TO_YMINTERVAL('-0-1')`          | -000000000-01                              |
| `TO_YMINTERVAL('1-0')`           | +000000001-00                              |
| `TO_YMINTERVAL('1-0')`           | -000000001-00                              |
| `TO_YMINTERVAL('0-11')`          | +000000000-11                              |
| `TO_YMINTERVAL('-0-11')`         | -000000000-11                              |
| `TO_YMINTERVAL('0-12')`          | ORA-01843: An invalid month was specified. |
| `TO_YMINTERVAL('999999999-11')`  | +999999999-11                              |
| `TO_YMINTERVAL('-999999999-11')` | -999999999-11                              |

---

## 2. INTERVAL DAY TO SECOND {#interval-day-to-second}

Gün, saat, dakika ve saniye bazında zaman aralığını belirtir.

| Syntax                                                          | Açıklama                                                                 |
|-----------------------------------------------------------------|--------------------------------------------------------------------------|
| `INTERVAL DAY[(hassasiyet)] TO SECOND[(hassasiyet)]`            | Veri tipini belirtir.                                                    |
| `INTERVAL 'g sa:dk:sn.kesirli_sn' DAY[(hassasiyet)] TO SECOND[(hassasiyet)]` | Gün, saat, dakika ve saniye bazlı tarih aralığı ifade eder. |
| `INTERVAL 'g sa:dk' DAY[(hassasiyet)] TO MINUTE`                | Gün, saat ve dakika bazlı tarih aralığı ifade eder.                      |
| `INTERVAL 'g sa' DAY[(hassasiyet)] TO HOUR`                     | Gün ve saat bazlı tarih aralığı ifade eder.                              |
| `INTERVAL 'g' DAY[(hassasiyet)]`                                | Gün bazlı tarih aralığı ifade eder.                                      |
| `INTERVAL 'sa:dk:sn.kesirli_sn' HOUR TO SECOND[(hassasiyet)]`   | Saat, dakika ve saniye bazlı tarih aralığı ifade eder.                   |
| `INTERVAL 'sa:dk' HOUR[(hassasiyet)] TO MINUTE`                 | Saat ve dakika bazlı tarih aralığı ifade eder.                           |
| `INTERVAL 'sa' HOUR[(hassasiyet)]`                              | Saat bazlı tarih aralığı ifade eder.                                     |
| `INTERVAL 'dk:sn' MINUTE[(hassasiyet)] TO SECOND[(hassasiyet)]` | Dakika ve saniye bazlı tarih aralığı ifade eder.                         |
| `INTERVAL 'dk' MINUTE[(hassasiyet)]`                            | Dakika bazlı tarih aralığı ifade eder.                                   |
| `INTERVAL 'sn.kesirli_sn' SECOND[(hassasiyet), (hassasiyet)]`   | Saniye bazlı tarih aralığı ifade eder.                                   |

- Gün hassasiyeti;
    - 0-9 arasında olabilir.
    - Varsayılan değeri 2'dir.
- Saat hassasiyeti;
    - 0-9 arasında olabilir.
    - Varsayılan değeri 3'tür.
- Dakika hassasiyeti;
    - 0-9 arasında olabilir.
    - Varsayılan değeri 4'tür.
- Saniye hassasiyeti;
    - Saniyenin ana kısmı için 0-9 arasında olabilir, varsayılan değeri 6'dır.
    - Saniyenin kesirli kısmı için de 0-9 arasında olabilir, varsayılan değeri 6'dır.

| Syntax                                                        | Açıklama                                               | Sonuç                         |
|---------------------------------------------------------------|--------------------------------------------------------|-------------------------------|
| `INTERVAL '999999999 23:59:59.999999999' DAY(9) TO SECOND(9)` | 999999999 gün, 23 saat, 59 dakika, 59.999999999 saniye | +999999999 23:59:59.999999999 |
| `INTERVAL '999999999 23:59' DAY(9) TO MINUTE`                 | 999999999 gün, 23 saat, 59 dakika                      | +999999999 23:59:00           |
| `INTERVAL '999999999 23' DAY(9) TO HOUR`                      | 999999999 gün, 23 saat                                 | +999999999 23:00:00           |
| `INTERVAL '999999999' DAY(9)`                                 | 999999999 gün                                          | +999999999 00:00:00           |
| `INTERVAL '00:00:00.000000' HOUR TO SECOND`                   | 0 saat, 0 dakika, 0 saniye                             | +00 00:00:00.000000           |
| `INTERVAL '00:00:00.999999' HOUR TO SECOND`                   | 0 saat, 0 dakika, 0.999999 saniye                      | +00 00:00:00.999999           |
| `INTERVAL '00:00:00.9999999' HOUR TO SECOND`                  | 0 saat, 1 dakika, 0 saniye                             | +00 00:00:01.000000           |
| `INTERVAL '23:59:59.999999999' HOUR TO SECOND(9)`             | 23 saat, 59 dakika, 59.999999999 saniye                | +00 23:59:59.999999999        |
| `INTERVAL '999999999:59' HOUR(9) TO MINUTE`                   | 999999999 saat, 59 dakika                              | +041666666 15:59:00           |
| `INTERVAL '0' HOUR`                                           | 0 saat                                                 | +00 00:00:00                  |
| `INTERVAL '999999999' HOUR(9)`                                | 999999999 saat                                         | +041666666 15:00:00           |
| `INTERVAL '999999999:59.999999999' MINUTE(9) TO SECOND(9)`    | 999999999 dakika, 59.999999999 saniye                  | +000694444 10:39:59.999999999 |
| `INTERVAL '0' MINUTE`                                         | 0 dakika                                               | +00 00:00:00                  |
| `INTERVAL '999999999' MINUTE(9)`                              | 999999999 dakika                                       | +000694444 10:39:00           |
| `INTERVAL '999999999.999999999' SECOND(9, 9)`                 | 999999999.999999999 saniye                             | +000011574 01:46:39.999999999 |

### 2.1 NUMTODSINTERVAL Fonksiyonu {#numtodsinterval}

Bir sayıyı `INTERVAL DAY TO SECOND` tipine çevirir.

| Syntax                                                    |
|-----------------------------------------------------------|
| ```NUMTODSINTERVAL(sayi, DAY | HOUR | MINUTE | SECOND)``` |

Aşağıdaki tabloda NUMTODSINTERVAL fonksiyonunun kullanım örnekleri bulunmaktadır.

| Kullanım                                 | Sonuç                         |
|------------------------------------------|-------------------------------|
| `NUMTODSINTERVAL(0, 'DAY')`              | +000000000 00:00:00.000000000 |
| `NUMTODSINTERVAL(1, 'DAY')`              | +000000001 00:00:00.000000000 |
| `NUMTODSINTERVAL(999999999, 'DAY')`      | +999999999 00:00:00.000000000 |
| `NUMTODSINTERVAL(0, 'HOUR')`             | +000000000 00:00:00.000000000 |
| `NUMTODSINTERVAL(1, 'HOUR')`             | +000000000 01:00:00.000000000 |
| `NUMTODSINTERVAL(23, 'HOUR')`            | +000000000 23:00:00.000000000 |
| `NUMTODSINTERVAL(24, 'HOUR')`            | +000000001 00:00:00.000000000 |
| `NUMTODSINTERVAL(0, 'MINUTE')`           | +000000000 00:00:00.000000000 |
| `NUMTODSINTERVAL(1, 'MINUTE')`           | +000000000 00:01:00.000000000 |
| `NUMTODSINTERVAL(59, 'MINUTE')`          | +000000000 00:59:00.000000000 |
| `NUMTODSINTERVAL(60, 'MINUTE')`          | +000000000 01:00:00.000000000 |
| `NUMTODSINTERVAL(0, 'SECOND')`           | +000000000 00:00:00.000000000 |
| `NUMTODSINTERVAL(1, 'SECOND')`           | +000000000 00:00:01.000000000 |
| `NUMTODSINTERVAL(1.999999999, 'SECOND')` | +000000000 00:00:01.999999999 |
| `NUMTODSINTERVAL(59, 'SECOND')`          | +000000000 00:00:59.000000000 |
| `NUMTODSINTERVAL(60, 'SECOND')`          | +000000000 00:01:00.000000000 |

### 2.2 TO_DSINTERVAL Fonksiyonu {#to_dsinterval}
