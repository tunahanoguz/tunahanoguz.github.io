---
title:  "Oracle - TO_DATE Fonksiyonu"
date: 2025-05-19 16:45:00 +0300
layout: post
categories: oracle
---

`TO_DATE` fonksiyonu, bir string'i `DATE` tipine dönüştürür ve yeni değeri döndürür.

| Syntax                                                                                      |
|---------------------------------------------------------------------------------------------|
| `TO_DATE(metin [DEFAULT deger ON CONVERSION ERROR] [,format] [,'NLS_DATE_LANGUAGE = dil'])` |

- `metin` isimli parametre, `DATE` tipine dönüştürülecek string ifadedir.
- `[DEFAULT deger ON CONVERSION ERROR]` ifadesi, dönüştürme işleminin hata alması durumunda fonksiyonun varsayılan bir değer dönmesini sağlar.
- `format` isimli parametre, string ifadenin hangi formatta olduğunu belirtir.
  - Bu parametre verilmezse, `initialization parameter` grubunda yer alan `NLS_DATE_FORMAT` ve `NLS_TERRITORY` parametrelerinin değerleri dikkate alınır.
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
| `D`              | x |
| `DD`             | Ayın gününü ifade eder.                              |
| `DDD`            | x |
| `MM`             | 2 haneli sayı olacak şekilde ayı ifade eder.         |
| `MON`            | Kısaltılmış ayı ifade eder.                          |
| `MONTH`          | Tam ay adını ifade eder.                             |
| `RM`             | x |
| `Y`              | x |
| `YY`             | x |
| `YYY`            | x |
| `YYYY`           | 4 haneli yıl bilgisini ifade eder.                   |
| `RRRR`           | 2 haneli veya 4 haneli yıl bilgisi kabul eder. 2 haneli yıl bilgisi belirtilmesi durumunda, ilk 2 hane, string ifadede belirtilen yıl 0-49 arasındaysa içinde bulunulan yüzyıl, 50-99 arasındaysa bir önceki yüzyıl ile tamamlanır.     |
| `AM` veya `A.M.` | x |
| `PM` veya `P.M.` | x |
| `BC` veya `B.C.` | x |
| `AD` veya `A.D.` | x |

- Gün belirtilmediğinde, gün bilgisi doğrudan **ayın 1'i** olarak belirlenir.
- Ay belirtilmediğinde, ay bilgisi doğrudan **yılın ilk ayı** olarak belirlenir.
- Yıl belirtilmediğinde, yıl bilgisi doğrudan **içinde bulunulan yıl** olarak belirlenir.
- Saat belirtilmediğinde;
  - 12 saatlik zaman diliminde saat bilgisi doğrudan **12** olarak belirlenir.
  - 24 saatlik zaman diliminde saat bilgisi doğrudan **00** olarak belirlenir.
- Dakika belirtilmediğinde, dakika bilgisi doğrudan **00** olarak belirlenir.
- Saniye belirtilmediğinde, saniye bilgisi doğrudan **00** olarak belirlenir.
- 12 saatlik zaman diliminde, AM/PM belirtilmediğinde, AM/PM bilgisi;
  - Saat bilgisi 12 olarak belirtildiyse doğrudan **PM** olarak belirlenir.
  - Saat belirtilmediyse, saat bilgisi doğrudan **12** olarak belirlendiği için, **PM** olarak belirlenir.
  - Saat bilgisi 12 dışında bir değer aldıysa doğrudan **AM** olarak belirlenir.

---

- Aşağıdaki tabloda `TO_DATE` fonksiyonu için kullanım örnekleri yer almaktadır.
- `NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS AM BC` olarak belirlenmiştir. (Ek bilgi; AM yerine PM de kullanılabilir. Format belirtilirken ikisi eşdeğerdir.)
- Sorgular 19.05.2025 tarihinde çalıştırılmıştır.

| Kullanım                              | Sonuç                                    |
|---------------------------------------|------------------------------------------|
| `TO_DATE('12', 'HH')`                 | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('11', 'HH')`                 | 01.05.2025 11:00:00 AM                   |
| `TO_DATE('12 AM', 'HH AM')`           | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('12 AM', 'HH PM')`           | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('00', 'HH')`                 | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('13', 'HH')`                 | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('12', 'HH12')`               | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('11', 'HH12')`               | 01.05.2025 11:00:00 AM                   |
| `TO_DATE('12 AM', 'HH12 AM')`         | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('12 AM', 'HH12 PM')`         | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('00', 'HH12')`               | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('13', 'HH12')`               | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('12', 'HH24')`               | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('00', 'HH24')`               | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('11', 'HH24')`               | 01.05.2025 11:00:00 AM                   |
| `TO_DATE('24', 'HH24')`               | ORA-01850: hour must be between 0 and 23 |
| `TO_DATE('2025', 'YYYY')`             | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('2024', 'YYYY')`             | 01.05.2024 12:00:00 AM                   |
| `TO_DATE('2025', 'RRRR')`             | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('2024', 'RRRR')`             | 01.05.2024 12:00:00 AM                   |
| `TO_DATE('0', 'RRRR')`                | 01.05.2000 12:00:00 AM                   |
| `TO_DATE('49', 'RRRR')`               | 01.05.2049 12:00:00 AM                   |
| `TO_DATE('50', 'RRRR')`               | 01.05.1950 12:00:00 AM                   |
| `TO_DATE('99', 'RRRR')`               | 01.05.1999 12:00:00 AM                   |
| `TO_DATE('100', 'RRRR')`              | 01.05.0100 12:00:00 AM                   |
| `TO_DATE('03.2025', 'MM.YYYY')`       | 01.03.2025 12:00:00 AM                   |
| `TO_DATE('03.2024', 'MM.YYYY')`       | 01.03.2024 12:00:00 AM                   |
| `TO_DATE('18.03', 'DD.MM')`           | 01.03.2025 12:00:00 AM                   |
| `TO_DATE('18.03.2025', 'DD.MM.YYYY')` | 18.03.2025 12:00:00 AM                   |
| `TO_DATE('18.03.2024', 'DD.MM.YYYY')` | 18.03.2024 12:00:00 AM                   |
| `SELECT TO_DATE('OCA', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.01.2025 12:00:00 AM                   |
| `SELECT TO_DATE('ŞUB', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.02.2025 12:00:00 AM                   |
| `SELECT TO_DATE('MAR', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.03.2025 12:00:00 AM                   |
| `SELECT TO_DATE('NİS', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.04.2025 12:00:00 AM                   |
| `SELECT TO_DATE('MAY', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.05.2025 12:00:00 AM                   |
| `SELECT TO_DATE('HAZ', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.06.2025 12:00:00 AM                   |
| `SELECT TO_DATE('TEM', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.07.2025 12:00:00 AM                   |
| `SELECT TO_DATE('AĞU', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.08.2025 12:00:00 AM                   |
| `SELECT TO_DATE('EYL', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.09.2025 12:00:00 AM                   |
| `SELECT TO_DATE('EKİ', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.10.2025 12:00:00 AM                   |
| `SELECT TO_DATE('KAS', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.11.2025 12:00:00 AM                   |
| `SELECT TO_DATE('ARA', 'MON', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.12.2025 12:00:00 AM                   |
| `SELECT TO_DATE('OCAK', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`    | 01.01.2025 12:00:00 AM                   |
| `SELECT TO_DATE('ŞUBAT', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`   | 01.02.2025 12:00:00 AM                   |
| `SELECT TO_DATE('MART', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`    | 01.03.2025 12:00:00 AM                   |
| `SELECT TO_DATE('NİSAN', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`   | 01.04.2025 12:00:00 AM                   |
| `SELECT TO_DATE('MAYIS', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`   | 01.05.2025 12:00:00 AM                   |
| `SELECT TO_DATE('HAZİRAN', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.06.2025 12:00:00 AM                   |
| `SELECT TO_DATE('TEMMUZ', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`  | 01.07.2025 12:00:00 AM                   |
| `SELECT TO_DATE('AĞUSTOS', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')` | 01.08.2025 12:00:00 AM                   |
| `SELECT TO_DATE('EYLÜL', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`   | 01.09.2025 12:00:00 AM                   |
| `SELECT TO_DATE('EKİM', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`    | 01.10.2025 12:00:00 AM                   |
| `SELECT TO_DATE('KASIM', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`   | 01.11.2025 12:00:00 AM                   |
| `SELECT TO_DATE('ARALIK', 'MONTH', 'NLS_DATE_LANGUAGE = TURKISH')`  | 01.12.2025 12:00:00 AM                   |
