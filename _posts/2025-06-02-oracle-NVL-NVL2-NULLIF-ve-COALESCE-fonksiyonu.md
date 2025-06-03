---
title:  "Oracle - NVL, NVL2, NULLIF ve COALESCE Fonksiyonu"
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

Aşağıdaki tabloda veritabanındaki `KISILER` tablosundaki veriler yer almaktadır.

```sql
CREATE TABLE KISILER (
    AD       VARCHAR2(1000 CHAR),
    SOYAD    VARCHAR2(1000 CHAR),
    SEHIR    VARCHAR2(1000 CHAR),
    YAS      NUMBER(3)
);
```

| AD     | SOYAD  | SEHIR    | YAS  |
|--------|--------|----------|------|
| Ahmet  | Çelik  | İstanbul | 30   |
| Mehmet | Demir  | Ankara   | NULL |
| Ayşe   | NULL   | İzmir    | 32   |
| Zeynep | Şahin  | Adana    | 36   |
| Mahmut | Çelik  | NULL     | 24   |
| Hazal  | Demir  | Aydın    | 22   |

Aşağıdaki tabloda `NVL` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç | Dönüş Tipi |
|----------|-------|------------|
| `SELECT NVL(SEHİR, 'Muğla') FROM KISILER`  | İstanbul, Ankara, İzmir, Adana, **Muğla**, Aydın | VARCHAR2 |
| `SELECT NVL(SEHİR, 10) FROM KISILER`       | İstanbul, Ankara, İzmir, Adana, 10, Aydın        | VARCHAR2 |
| `SELECT NVL(YAS, SEHİR) FROM KISILER`      | ORA-01722: unable to convert string value containing UNISTR('\FFFD') to a number: SEHIR<br>ORA-03302: (ORA-01722 details) invalid string value: Ankara                                                                                   | VARCHAR2 |
| `SELECT NVL(SOYAD, 'Yılmaz') FROM KISILER` | Çelik, Demir, **Yılmaz**, Şahin, Çelik, Demir    | VARCHAR2 |
| `SELECT NVL(YAS, 28) FROM KISILER`         | 30, **28**, 32, 36, 24, 22                       | NUMBER   |

---

- `NVL2` fonksiyonu, bir değerin `NULL` olduğu ve olmadığı durumlar için birer değer belirlenmesini sağlar.
- Değerin `NULL` olduğu ve olmadığı durumlar için belirtilen değerler `LONG` dışında herhangi bir tipte olabilir.
  - Ancak, bu iki değerin tipi ya aynı olmalı ya da implicit conversion ile birbirlerine dönüştürülebilir olmalıdır. Aksi durumda hata alınır.

| Syntax                                            |
|---------------------------------------------------|
| `NVL2(deger, null_degilse_deger, null_ise_deger)` |

Aşağıdaki tabloda `NVL2` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |

---

- `NULLIF` fonksiyonu, iki değeri birbiriyle karşılaştırır. Birbirlerine eşitse `NULL`, değilse birinci değeri döndürür.

| Syntax                     |
|----------------------------|
| `NULLIF(deger_1, deger_2)` |

Aşağıdaki tabloda `NULLIF` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |

---

- `COALESCE` fonksiyonu, **n** sayıda değerden ilk `NULL` olmayan değeri döndürür.

| Syntax                                     |
|--------------------------------------------|
| `COALESCE(deger_1, deger_2, ..., deger_n)` |

Aşağıdaki tabloda `COALESCE` fonksiyonu için kullanım örnekleri yer almaktadır.

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |
