---
title:  "Oracle - SESSIONTIMEZONE ve DBTIMEZONE Fonksiyonu"
date: 2025-05-31 16:15:00 +0300
layout: post
categories: oracle
---

- `SESSIONTIMEZONE` fonksiyonu, kullanıcı oturumundaki zaman dilimini (time zone) döndürür.
- `DBTIMEZONE` fonksiyonu, veritabanının zaman dilimini (time zone) döndürür.
- Her iki fonksiyon için de dönülen değer VARCHAR2 tipindedir.
- Her iki fonksiyon için de dönüş formatı, `CREATE DATABASE` veya `ALTER DATABASE` üzerinden veritabanının zaman diliminin nasıl belirtildiğine göre değişiklik gösterebilir. Time zone offset ([+|-]TZH:TZM) veya zaman dilimi adı iki olası dönüş formatıdır.

| Syntax            |
|-------------------|
| `SESSIONTIMEZONE` |
| `DBTIMEZONE`      |

---

Aşağıdaki tabloda `SESSIONTIMEZONE` ve `DBTIMEZONE` fonksiyonları için kullanım örnekleri yer almaktadır.

| Kullanım          | Sonuç           |
|-------------------|-----------------|
| `SESSIONTIMEZONE` | +00:00          |
| `DBTIMEZONE`      | +00:00          |
| `SESSIONTIMEZONE` | Europe/Istanbul |
| `DBTIMEZONE`      | Europe/Paris    |
