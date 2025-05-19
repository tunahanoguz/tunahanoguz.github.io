---
title:  "Oracle - TO_DATE Fonksiyonu"
date: 2025-05-19 16:45:00 +0300
layout: post
categories: oracle
---

`TO_DATE` fonksiyonu, bir string'i `DATE` tipine dönüştürür ve yeni değeri döndürür.

| Syntax                                                                                      |
|---------------------------------------------------------------------------------------------|
| `TO_DATE(metin [DEFAULT deger ON CONVERSION ERROR], [format], ['NLS_DATE_LANGUAGE = dil'])` |

- `metin` isimli parametre, `DATE` tipine dönüştürülecek string ifadedir.
- `[DEFAULT deger ON CONVERSION ERROR]` ifadesi, dönüştürme işleminin hata alması durumunda fonksiyonun varsayılan bir değer dönmesini sağlar.
- `format` isimli parametre, string ifadenin hangi formatta olduğunu belirtir.
  - Bu parametre verilmezse, `initialization parameter` grubunda yer alan `NLS_DATE_FORMAT` ve `NLS_TERRITORY` parametrelerinin değerleri dikkate alınır.
- `['NLS_DATE_LANGUAGE = dil']` ifadesi, string ifadenin hangi dilde olduğunu belirtir.

Aşağıdaki tabloda `format` isim parametrenin alabileceği değerler ve onların açıklamaları yer almaktadır.

| Format           | Açıklama |
|------------------|----------|
| `HH`             | 12 saatlik zaman diliminde günün saatini ifade eder. |
| `HH12`           | 12 saatlik zaman diliminde günün saatini ifade eder. |
| `HH24`           | 24 saatlik zaman diliminde günün saatini ifade eder. |
| `MI`             | Dakikayı ifade eder. |
| `SS`             | Saniyeyi ifade eder. |
| `DD`             | Ayın gününü ifade eder. |

Aşağıdaki tabloda `TO_DATE` fonksiyonu için kullanım örnekleri yer almaktadır.
`NLS_DATE_FORMAT` değeri `DD.MM.YYYY HH12:MI:SS AM` olarak belirlenmiştir. (Ek bilgi; AM yerine PM de kullanılabilir. Format belirtilirken ikisi eşdeğerdir.)

| Kullanım                      | Sonuç                                    |
|-------------------------------|------------------------------------------|
| `TO_DATE('12', 'HH')`         | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('12 AM', 'HH AM')`   | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('12 AM', 'HH PM')`   | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('00', 'HH')`         | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('13', 'HH')`         | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('12', 'HH12')`       | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('12 AM', 'HH12 AM')` | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('12 AM', 'HH12 PM')` | 01.05.2025 12:00:00 AM                   |
| `TO_DATE('00', 'HH12')`       | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('13', 'HH12')`       | ORA-01849: hour must be between 1 and 12 |
| `TO_DATE('12', 'HH24')`       | 01.05.2025 12:00:00 PM                   |
| `TO_DATE('24', 'HH24')`       | ORA-01850: hour must be between 0 and 23 |
