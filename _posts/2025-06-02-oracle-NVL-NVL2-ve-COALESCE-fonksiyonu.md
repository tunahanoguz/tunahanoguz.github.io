---
title:  "Oracle - NVL, NVL2 ve COALESCE Fonksiyonu"
date: 2025-06-02 21:30:00 +0300
layout: post
categories: oracle
---

- `NVL` fonksiyonu, `NULL` bir değer için alternatif bir değer belirlenmesini sağlar.
- Değerin tipi ile alternatif olarak belirtilen değerin tipi ya aynı olmalı ya da implicit conversion ile birbirine dönüştürülebilir olmalıdır. Aksi durumda hata alınır.
- Dönüş tipi, ilk değer ile aynı tiptedir.

| Syntax                         |
|--------------------------------|
| `NVL(deger, alternatif_deger)` |

---

- `NVL2` fonksiyonu, bir değerin `NULL` olduğu ve olmadığı durumlar için birer değer belirlenmesini sağlar.
- Değerin `NULL` olduğu ve olmadığı durumlar için belirtilen değerler `LONG` dışında herhangi bir tipte olabilir.
  - Ancak, bu iki değerin tipi ya aynı olmalı ya da implicit conversion ile birbirlerine dönüştürülebilir olmalıdır. Aksi durumda hata alınır.

| Syntax                                            |
|---------------------------------------------------|
| `NVL2(deger, null_degilse_deger, null_ise_deger)` |

---

- `COALESCE` fonksiyonu, **n** sayıda değerden ilk `NULL` olmayan değeri döndürür.

| Syntax                                     |
|--------------------------------------------|
| `COALESCE(deger_1, deger_2, ..., deger_n)` |
