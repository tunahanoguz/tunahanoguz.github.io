---
title:  "Oracle - NEW_TIME Fonksiyonu"
date: 2025-05-23 19:30:00 +0300
layout: post
categories: oracle
---

`NEW_TIME` fonksiyonu, bir zaman dilimindeki bir tarihi başka bir zaman diliminde bir tarihe dönüştürür ve yeni tarihi döner.

| Syntax                                                      |
|-------------------------------------------------------------|
| `NEW_TIME(tarih, orijinal_zaman_dilimi, yeni_zaman_dilimi)` |

- `tarih` parametresi, dönüşüme konu olan tarih değeridir.
- `orijinal_zaman_dilimi` parametresi, `tarih` parametresinin zaman dilimini ifade eder.
- `yeni_zaman_dilimi` parametresi, dönüşüm yapılacak yeni zaman dilimidir.

Her iki zaman dilimi için de kullanılabilecek zaman dilimleri aşağıdaki tabloda yer almaktadır:

| Değer | Açıklama                    |
|-------|-----------------------------|
| AST	  | Atlantic Standard Time      |
| ADT	  | Atlantic Daylight Time      |
| BST	  | Bering Standard Time        |
| BDT	  | Bering Daylight Time        |
| CST	  | Central Standard Time       |
| CDT	  | Central Daylight Time       |
| EST	  | Eastern Standard Time       |
| EDT	  | Eastern Daylight Time       |
| GMT	  | Greenwich Mean Time         |
| HST	  | Alaska-Hawaii Standard Time |
| HDT	  | Alaska-Hawaii Daylight Time |
| MST	  | Mountain Standard Time      |
| MDT	  | Mountain Daylight Time      |
| NST	  | Newfoundland Standard Time  |
| PST	  | Pacific Standard Time       |
| PDT	  | Pacific Daylight Time       |
| YST	  | Yukon Standard Time         |
| YDT	  | Yukon Daylight Time         |

---

| Kullanım | Sonuç |
|----------|-------|
| x        | x     |
