---
title:  "Oracle - EXTRACT Fonksiyonu"
date: 2025-05-26 19:45:00 +0300
layout: post
categories: oracle
---

`EXTRACT` fonksiyonu, `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE` ve `INTERVAL` tipindeki bir veriden bazı bilgilerin elde edilmesini sağlar.
Aşağıdaki tabloda bu bilgiler ve bu bilgilerin hangi tipteki verilerden elde edilebileceği yer almaktadır.

| Bilgi             | DATE | TIMESTAMP | TIMESTAMP WITH TIME ZONE | INTERVAL |
|-------------------|------|-----------|--------------------------|----------|
| `YEAR`            | 🟢   | 🟢        | 🟢                        | 🟢       |
| `MONTH`           | 🟢   | 🟢        | 🟢                        | 🟢       |
| `DAY`             | 🟢   | 🟢        | 🟢                        | 🟢       |
| `HOUR`            | 🔴   | 🟢        | 🟢                        | 🟢       |
| `MINUTE`          | 🔴   | 🟢        | 🟢                        | 🟢       |
| `SECOND`          | 🔴   | 🟢        | 🟢                        | 🟢       |
| `TIMEZONE_HOUR`   | 🔴   | 🟢        | 🟢                        | 🟢       |
| `TIMEZONE_MINUTE` | 🔴   | 🟢        | 🟢                        | 🟢       |
| `TIMEZONE_REGION` | 🔴   | 🟢        | 🟢                        | 🟢       |
| `TIMEZONE_ABBR`   | 🔴   | 🟢        | 🟢                        | 🟢       |
