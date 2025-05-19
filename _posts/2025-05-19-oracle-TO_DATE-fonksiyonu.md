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

| Format | Açıklama |
|--------|----------|
| x      | x        |

Aşağıdaki tabloda `TO_DATE` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |
