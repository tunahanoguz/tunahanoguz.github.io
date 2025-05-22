---
title:  "Oracle - TO_TIMESTAMP Fonksiyonu"
date: 2025-05-22 20:45:00 +0300
layout: post
categories: oracle
---

`TO_TIMESTAMP` fonksiyonu, bir string'i `TIMESTAMP` tipine dönüştürür ve yeni değeri döndürür.

| Syntax                                                                                           |
|--------------------------------------------------------------------------------------------------|
| `TO_TIMESTAMP(metin [DEFAULT deger ON CONVERSION ERROR] [,format] [,'NLS_DATE_LANGUAGE = dil'])` |

- `metin` isimli parametre, `DATE` tipine dönüştürülecek string ifadedir.
- `[DEFAULT deger ON CONVERSION ERROR]` ifadesi, dönüştürme işleminin hata alması durumunda, `metin` isimli parametre için varsayılan bir değer belirler. Dönüştürme işlemi bu varsayılan değere göre yapılır.
- `format` isimli parametre, string ifadenin hangi formatta olduğunu belirtir.
  - Bu parametre verilmezse, `initialization parameter` grubunda yer alan `NLS_TIMESTAMP_FORMAT` ve `NLS_TERRITORY` parametrelerinin değerleri dikkate alınır.
- `['NLS_DATE_LANGUAGE = dil']` ifadesi, string ifadenin hangi dilde olduğunu belirtir.

---

Aşağıdaki tabloda `format` isim parametrenin alabileceği değerler ve onların açıklamaları yer almaktadır.

| Format           | Açıklama                                             |
|------------------|------------------------------------------------------|
| `HH`             | 12 saatlik zaman diliminde günün saatini ifade eder. |
| `HH12`           | 12 saatlik zaman diliminde günün saatini ifade eder. |
| `HH24`           | 24 saatlik zaman diliminde günün saatini ifade eder. |
| `MI`             | Dakikayı ifade eder.                                 |
| `SS`             | Saniyeyi ifade eder.                                 |
| `FF`             | Saniyenin kesirli kısmını ifade eder.                |
| `AM` veya `A.M.` | Öğleden önce veya öğleden sonra ifadesidir.          |
| `PM` veya `P.M.` | Öğleden önce veya öğleden sonra ifadesidir.          |
| `D`              | Haftanın bir gününü ifade eder. (1-7) Tek başına yeterli değildir, daha ayrıntılı bir tarih bilgisinin parçası olarak kullanılabilir ve bu tarih bilgisiyle uyumlu olmalıdır. `NLS_TERRITORY` initialization parametresinin değerine göre haftanın başlangıç-bitiş günü değişebilir. (AMERICA -> {1, SUNDAY}, TURKEY -> {1, PAZARTESİ}) |
| `DD`             | Ayın bir gününü ifade eder. (1-31)                   |
| `DY`             | Haftanın bir gününü, kısaltılmış haliyle ifade eder. Tek başına yeterli değildir, daha ayrıntılı bir tarih bilgisinin parçası olarak kullanılabilir ve bu tarih bilgisiyle uyumlu olmalıdır. |
| `DAY`            | Haftanın bir gününü, adının tam haliyle ifade eder. Tek başına yeterli değildir, daha ayrıntılı bir tarih bilgisinin parçası olarak kullanılabilir ve bu tarih bilgisiyle uyumlu olmalıdır.  |
| `DDD`            | Yılın bir gününü ifade eder. (1-366)                 |
| `MM`             | 2 haneli sayı olacak şekilde ayı ifade eder.         |
| `MON`            | Ay bilgisini, adı kısaltılmış şekliyle ifade eder.   |
| `MONTH`          | Ay bilgisini, adının tam şekliyle ifade eder.        |
| `RM`             | Roma rakamlarıyla ayı ifade eder.                    |
| `Y`              | Yılın son 1 hanesini ifade eder.                     |
| `YY`             | Yılın son 2 hanesini ifade eder.                     |
| `YYY`            | Yılın son 3 hanesini ifade eder.                     |
| `YYYY`           | 4 haneli yıl bilgisini ifade eder.                   |
| `RRRR`           | 2 haneli veya 4 haneli yıl bilgisi kabul eder. 2 haneli yıl bilgisi belirtilmesi durumunda, ilk 2 hane, string ifadede belirtilen yıl 0-49 arasındaysa içinde bulunulan yüzyıl, 50-99 arasındaysa bir önceki yüzyıl ile tamamlanır.                                                           |
| `BC` veya `B.C.` | Milattan önce veya milattan sonra ifadesidir.        |
| `AD` veya `A.D.` | Milattan önce veya milattan sonra ifadesidir.        |
| `J`              | Jülyen günü; MÖ 4712 yılı 1 Ocak'ından bu yana geçen gün sayısıdır. |
| `SSSSS`          | Gece yarısından sonra geçen saniyelerdir. (0-86399)  |

- Gün belirtilmediğinde, gün bilgisi doğrudan **ayın 1'i** olarak belirlenir.
- Ay belirtilmediğinde, ay bilgisi doğrudan **yılın ilk ayı** olarak belirlenir.
- Yıl belirtilmediğinde, yıl bilgisi doğrudan **içinde bulunulan yıl** olarak belirlenir.
- Saat belirtilmediğinde;
  - 12 saatlik zaman diliminde saat bilgisi doğrudan **12** olarak belirlenir.
  - 24 saatlik zaman diliminde saat bilgisi doğrudan **00** olarak belirlenir.
- Dakika belirtilmediğinde, dakika bilgisi doğrudan **00** olarak belirlenir.
- Saniye belirtilmediğinde, saniye bilgisi doğrudan **00** olarak belirlenir.
- Saniyenin kesirli kısmı belirtilmediğinde, doğrudan **000000000** olarak belirlenir.
- 12 saatlik zaman diliminde, AM/PM belirtilmediğinde, AM/PM bilgisi;
  - Saat bilgisi 12 olarak belirtildiyse doğrudan **PM** olarak belirlenir.
  - Saat belirtilmediyse, saat bilgisi doğrudan **12** olarak belirlendiği için, **PM** olarak belirlenir.
  - Saat bilgisi 12 dışında bir değer aldıysa doğrudan **AM** olarak belirlenir.

---

- Aşağıdaki tabloda `TO_TIMESTAMP` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS.FF AM BC` olarak belirlenmiştir.
- Sorgular 19.05.2025 tarihinde çalıştırılmıştır.

| Kullanım                                                                    | Sonuç                                    |
|-----------------------------------------------------------------------------|------------------------------------------|
| `TO_TIMESTAMP('12', 'HH')`                                                       | 01.05.2025 12:00:00 PM AD                |
| `TO_TIMESTAMP('11', 'HH')`                                                       | 01.05.2025 11:00:00 AM AD                |
| `TO_TIMESTAMP('12 AM', 'HH AM')`                                                 | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('12 AM', 'HH PM')`                                                 | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('00', 'HH')`                                                       | ORA-01849: hour must be between 1 and 12 |
| `TO_TIMESTAMP('13', 'HH')`                                                       | ORA-01849: hour must be between 1 and 12 |
| `TO_TIMESTAMP('12', 'HH12')`                                                     | 01.05.2025 12:00:00 PM AD                |
| `TO_TIMESTAMP('11', 'HH12')`                                                     | 01.05.2025 11:00:00 AM AD                |
| `TO_TIMESTAMP('12 AM', 'HH12 AM')`                                               | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('12 AM', 'HH12 PM')`                                               | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('00', 'HH12')`                                                     | ORA-01849: hour must be between 1 and 12 |
| `TO_TIMESTAMP('13', 'HH12')`                                                     | ORA-01849: hour must be between 1 and 12 |
| `TO_TIMESTAMP('12', 'HH24')`                                                     | 01.05.2025 12:00:00 PM AD                |
| `TO_TIMESTAMP('00', 'HH24')`                                                     | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('11', 'HH24')`                                                     | 01.05.2025 11:00:00 AM AD                |
| `TO_TIMESTAMP('23', 'HH24')`                                                     | 01.05.2025 11:00:00 PM AD                |
| `TO_TIMESTAMP('24', 'HH24')`                                                     | ORA-01850: hour must be between 0 and 23 |
| `TO_TIMESTAMP('38', 'MI')`                                                       | 01.05.2025 12:38:00 AM AD                |
| `TO_TIMESTAMP('47', 'SS')`                                                       | 01.05.2025 12:00:47 AM AD                |
| `TO_TIMESTAMP('1', 'FF')`                                                        | 01.05.2025 12:00:00.100000000 AM AD      |
| `TO_TIMESTAMP('01', 'FF')`                                                       | 01.05.2025 12:00:00.010000000 AM AD      |
| `TO_TIMESTAMP('001', 'FF')`                                                      | 01.05.2025 12:00:00.001000000 AM AD      |
| `TO_TIMESTAMP('0001', 'FF')`                                                     | 01.05.2025 12:00:00.000100000 AM AD      |
| `TO_TIMESTAMP('00001', 'FF')`                                                    | 01.05.2025 12:00:00.000010000 AM AD      |
| `TO_TIMESTAMP('000001', 'FF')`                                                   | 01.05.2025 12:00:00.000001000 AM AD      |
| `TO_TIMESTAMP('0000001', 'FF')`                                                  | 01.05.2025 12:00:00.000000100 AM AD      |
| `TO_TIMESTAMP('00000001', 'FF')`                                                 | 01.05.2025 12:00:00.000000010 AM AD      |
| `TO_TIMESTAMP('000000001', 'FF')`                                                | 01.05.2025 12:00:00.000000001 AM AD      |
| `TO_TIMESTAMP('999999999', 'FF')`                                                | 01.05.2025 12:00:00.999999999 AM AD      |
| `TO_TIMESTAMP('16:38:47', 'HH24:MI:SS')`                                         | 01.05.2025 04:38:47 AM AD                |
| `TO_TIMESTAMP('16:38:47 1', 'HH24:MI:SS FF')`                                    | 01.05.2025 12:00:00.100000000 AM AD      |
| `TO_TIMESTAMP('16:38:47 01', 'HH24:MI:SS FF')`                                   | 01.05.2025 12:00:00.010000000 AM AD      |
| `TO_TIMESTAMP('16:38:47 001', 'HH24:MI:SS FF')`                                  | 01.05.2025 12:00:00.001000000 AM AD      |
| `TO_TIMESTAMP('16:38:47 0001', 'HH24:MI:SS FF')`                                 | 01.05.2025 12:00:00.000100000 AM AD      |
| `TO_TIMESTAMP('16:38:47 00001', 'HH24:MI:SS FF')`                                | 01.05.2025 12:00:00.000010000 AM AD      |
| `TO_TIMESTAMP('16:38:47 000001', 'HH24:MI:SS FF')`                               | 01.05.2025 12:00:00.000001000 AM AD      |
| `TO_TIMESTAMP('16:38:47 0000001', 'HH24:MI:SS FF')`                              | 01.05.2025 12:00:00.000000100 AM AD      |
| `TO_TIMESTAMP('16:38:47 00000001', 'HH24:MI:SS FF')`                             | 01.05.2025 12:00:00.000000010 AM AD      |
| `TO_TIMESTAMP('16:38:47 000000001', 'HH24:MI:SS FF')`                            | 01.05.2025 12:00:00.000000001 AM AD      |
| `TO_TIMESTAMP('16:38:47 999999999', 'HH24:MI:SS FF')`                            | 01.05.2025 12:00:00.999999999 AM AD      |
| `TO_TIMESTAMP('1', 'DD')`                                                        | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('15', 'DD')`                                                       | 15.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('30', 'DD')`                                                       | 30.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('31', 'DD')`                                                       | 31.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('1', 'DDD')`                                                       | 01.01.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('10', 'DDD')`                                                      | 10.01.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('31', 'DDD')`                                                      | 31.01.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('364', 'DDD')`                                                     | 30.12.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('365', 'DDD')`                                                     | 31.12.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('0', 'Y')`                                                         | 01.05.2020 12:00:00 AM AD                |
| `TO_TIMESTAMP('1', 'Y')`                                                         | 01.05.2021 12:00:00 AM AD                |
| `TO_TIMESTAMP('2', 'Y')`                                                         | 01.05.2022 12:00:00 AM AD                |
| `TO_TIMESTAMP('3', 'Y')`                                                         | 01.05.2023 12:00:00 AM AD                |
| `TO_TIMESTAMP('4', 'Y')`                                                         | 01.05.2024 12:00:00 AM AD                |
| `TO_TIMESTAMP('5', 'Y')`                                                         | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('6', 'Y')`                                                         | 01.05.2026 12:00:00 AM AD                |
| `TO_TIMESTAMP('7', 'Y')`                                                         | 01.05.2027 12:00:00 AM AD                |
| `TO_TIMESTAMP('8', 'Y')`                                                         | 01.05.2028 12:00:00 AM AD                |
| `TO_TIMESTAMP('9', 'Y')`                                                         | 01.05.2029 12:00:00 AM AD                |
| `TO_TIMESTAMP('0', 'YY')`                                                        | 01.05.2000 12:00:00 AM AD                |
| `TO_TIMESTAMP('1', 'YY')`                                                        | 01.05.2001 12:00:00 AM AD                |
| `TO_TIMESTAMP('2', 'YY')`                                                        | 01.05.2002 12:00:00 AM AD                |
| `TO_TIMESTAMP('3', 'YY')`                                                        | 01.05.2003 12:00:00 AM AD                |
| `TO_TIMESTAMP('4', 'YY')`                                                        | 01.05.2004 12:00:00 AM AD                |
| `TO_TIMESTAMP('5', 'YY')`                                                        | 01.05.2005 12:00:00 AM AD                |
| `TO_TIMESTAMP('6', 'YY')`                                                        | 01.05.2006 12:00:00 AM AD                |
| `TO_TIMESTAMP('7', 'YY')`                                                        | 01.05.2007 12:00:00 AM AD                |
| `TO_TIMESTAMP('8', 'YY')`                                                        | 01.05.2008 12:00:00 AM AD                |
| `TO_TIMESTAMP('9', 'YY')`                                                        | 01.05.2009 12:00:00 AM AD                |
| `TO_TIMESTAMP('49', 'YY')`                                                       | 01.05.2049 12:00:00 AM AD                |
| `TO_TIMESTAMP('50', 'YY')`                                                       | 01.05.2050 12:00:00 AM AD                |
| `TO_TIMESTAMP('99', 'YY')`                                                       | 01.05.2099 12:00:00 AM AD                |
| `TO_TIMESTAMP('0', 'YYY')`                                                       | 01.05.2000 12:00:00 AM AD                |
| `TO_TIMESTAMP('1', 'YYY')`                                                       | 01.05.2001 12:00:00 AM AD                |
| `TO_TIMESTAMP('2', 'YYY')`                                                       | 01.05.2002 12:00:00 AM AD                |
| `TO_TIMESTAMP('3', 'YYY')`                                                       | 01.05.2003 12:00:00 AM AD                |
| `TO_TIMESTAMP('4', 'YYY')`                                                       | 01.05.2004 12:00:00 AM AD                |
| `TO_TIMESTAMP('5', 'YYY')`                                                       | 01.05.2005 12:00:00 AM AD                |
| `TO_TIMESTAMP('6', 'YYY')`                                                       | 01.05.2006 12:00:00 AM AD                |
| `TO_TIMESTAMP('7', 'YYY')`                                                       | 01.05.2007 12:00:00 AM AD                |
| `TO_TIMESTAMP('8', 'YYY')`                                                       | 01.05.2008 12:00:00 AM AD                |
| `TO_TIMESTAMP('9', 'YYY')`                                                       | 01.05.2009 12:00:00 AM AD                |
| `TO_TIMESTAMP('49', 'YYY')`                                                      | 01.05.2049 12:00:00 AM AD                |
| `TO_TIMESTAMP('50', 'YYY')`                                                      | 01.05.2050 12:00:00 AM AD                |
| `TO_TIMESTAMP('99', 'YYY')`                                                      | 01.05.2099 12:00:00 AM AD                |
| `TO_TIMESTAMP('100', 'YYY')`                                                     | 01.05.2100 12:00:00 AM AD                |
| `TO_TIMESTAMP('999', 'YYY')`                                                     | 01.05.2999 12:00:00 AM AD                |
| `TO_TIMESTAMP('2025', 'YYYY')`                                                   | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('2024', 'YYYY')`                                                   | 01.05.2024 12:00:00 AM AD                |
| `TO_TIMESTAMP('2025', 'RRRR')`                                                   | 01.05.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('2024', 'RRRR')`                                                   | 01.05.2024 12:00:00 AM AD                |
| `TO_TIMESTAMP('0', 'RRRR')`                                                      | 01.05.2000 12:00:00 AM AD                |
| `TO_TIMESTAMP('49', 'RRRR')`                                                     | 01.05.2049 12:00:00 AM AD                |
| `TO_TIMESTAMP('50', 'RRRR')`                                                     | 01.05.1950 12:00:00 AM AD                |
| `TO_TIMESTAMP('99', 'RRRR')`                                                     | 01.05.1999 12:00:00 AM AD                |
| `TO_TIMESTAMP('100', 'RRRR')`                                                    | 01.05.0100 12:00:00 AM AD                |
| `TO_TIMESTAMP('03.2025', 'MM.YYYY')`                                             | 01.03.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('03.2024', 'MM.YYYY')`                                             | 01.03.2024 12:00:00 AM AD                |
| `TO_TIMESTAMP('18.03', 'DD.MM')`                                                 | 01.03.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('18.03.2025', 'DD.MM.YYYY')`                                       | 18.03.2025 12:00:00 AM AD                |
| `TO_TIMESTAMP('18.03.2024', 'DD.MM.YYYY')`                                       | 18.03.2024 12:00:00 AM AD                |
| `TO_TIMESTAMP('OCA', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.01.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('ŞUB', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.02.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('MAR', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.03.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('NİS', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.04.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('MAY', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('HAZ', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.06.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('TEM', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.07.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('AĞU', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.08.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('EYL', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.09.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('EKİ', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.10.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('KAS', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.11.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('ARA', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')`                      | 01.12.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('OCAK', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                   | 01.01.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('ŞUBAT', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                  | 01.02.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('MART', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                   | 01.03.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('NİSAN', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                  | 01.04.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('MAYIS', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                  | 01.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('HAZİRAN', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                | 01.06.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('TEMMUZ', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                 | 01.07.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('AĞUSTOS', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                | 01.08.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('EYLÜL', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                  | 01.09.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('EKİM', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                   | 01.10.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('KASIM', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                  | 01.11.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('ARALIK', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`                 | 01.12.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('I', 'RM')`                                                        | 01.01.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('II', 'RM')`                                                       | 01.02.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('III', 'RM')`                                                      | 01.03.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('IV', 'RM')`                                                       | 01.04.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('V', 'RM')`                                                        | 01.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('VI', 'RM')`                                                       | 01.06.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('VII', 'RM')`                                                      | 01.07.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('VIII', 'RM')`                                                     | 01.08.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('IX', 'RM')`                                                       | 01.09.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('X', 'RM')`                                                        | 01.10.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('XI', 'RM')`                                                       | 01.11.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('XII', 'RM')`                                                      | 01.12.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('1', 'J')`                                                         | 01.01.4712 12:00:00 AM BC                  |
| `TO_TIMESTAMP('2', 'J')`                                                         | 02.01.4712 12:00:00 AM BC                  |
| `TO_TIMESTAMP('3', 'J')`                                                         | 03.01.4712 12:00:00 AM BC                  |
| `TO_TIMESTAMP('365', 'J')`                                                       | 31.12.4712 12:00:00 AM BC                  |
| `TO_TIMESTAMP('366', 'J')`                                                       | 01.01.4711 12:00:00 AM BC                  |
| `TO_TIMESTAMP('0', 'SSSSS')`                                                     | 01.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('1', 'SSSSS')`                                                     | 01.05.2025 12:00:01 AM AD                  |
| `TO_TIMESTAMP('2', 'SSSSS')`                                                     | 01.05.2025 12:00:02 AM AD                  |
| `TO_TIMESTAMP('60', 'SSSSS')`                                                    | 01.05.2025 12:01:00 AM AD                  |
| `TO_TIMESTAMP('86399', 'SSSSS')`                                                 | 01.05.2025 11:59:59 PM AD                  |
| `TO_TIMESTAMP('19.05.2025 PZT', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 19.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('19.05.2025 SAL', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | ORA-01835: day of week conflicts with Julian date |
| `TO_TIMESTAMP('20.05.2025 SAL', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 20.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('21.05.2025 ÇAR', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 21.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('22.05.2025 PER', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 22.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('23.05.2025 CUM', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 23.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('24.05.2025 CMT', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 24.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('25.05.2025 PAZ', 'DD.MM.YYYY DY', 'NLS_DATE_LANGUAGE = TURKISH')` | 25.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('19.05.2025 PAZARTESİ', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')` | 19.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('19.05.2025 SALI', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`      | ORA-01835: day of week conflicts with Julian date |
| `TO_TIMESTAMP('20.05.2025 SALI', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`      | 20.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('21.05.2025 ÇARŞAMBA', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`  | 21.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('22.05.2025 PERŞEMBE', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`  | 22.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('23.05.2025 CUMA', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`      | 23.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('24.05.2025 CUMARTESİ', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')` | 24.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('25.05.2025 PAZAR', 'DD.MM.YYYY DAY', 'NLS_DATE_LANGUAGE = TURKISH')`     | 25.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('19.05.2025 1', 'DD.MM.YYYY D')`                                   | 19.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('19.05.2025 2', 'DD.MM.YYYY D')`                                   | ORA-01835: day of week conflicts with Julian date |
| `TO_TIMESTAMP('20.05.2025 2', 'DD.MM.YYYY D')`                                   | 20.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('21.05.2025 3', 'DD.MM.YYYY D')`                                   | 21.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('22.05.2025 4', 'DD.MM.YYYY D')`                                   | 22.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('23.05.2025 5', 'DD.MM.YYYY D')`                                   | 23.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('24.05.2025 6', 'DD.MM.YYYY D')`                                   | 24.05.2025 12:00:00 AM AD                  |
| `TO_TIMESTAMP('25.05.2025 7', 'DD.MM.YYYY D')`                                   | 25.05.2025 12:00:00 AM AD                  |
