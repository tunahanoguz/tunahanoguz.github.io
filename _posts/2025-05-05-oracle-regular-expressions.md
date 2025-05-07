---
title:  "Oracle - Regular Expressions"
layout: post
categories: oracle
---

Regular expression (düzenli ifade), bir metindeki eşleşme desenini ifade eden karakter dizisidir. Regex ve regexp olarak kısaltılabilir. Regular expression, ifade ettiği desen ile genel olarak bir metin üzerinde arama yapmak, eşleşen kısmı metinden elde etmek ve düzenlemek için kullanılır.

Birçok yazılım dilinde ve o yazılım dilinde kullanılan modül/paket/kütüphanelerde regular expression için özel fonksiyonlar bulunur. Bu fonksiyonların isimleri, aldıkları parametreler ve regular expression desenindeki standartlar her yazılım dili/modül/paket/kütüphanede farklılaşabilir. Örneğin, positive lookahead ve negative lookahead gibi yapılar şimdilik Oracle üzerinde çalışmıyor. ```[:KARAKTERSINIFIADI:]``` yapısındaki POSIX karakter sınıfları Oracle'da kullanılabilirken, Python'ın yerleşik regular expression modülü olan ```re```'de kullanılamaz. Kullanabilmek için ```regex``` modülünü yüklemek gerekir. Ben bu yazıda regular expression konusunu Oracle odaklı olarak işleyeceğim.

Aşağıdaki tabloda, REGEXP_INSTR, REGEXP_COUNT, REGEXP_LIKE, REGEXP_SUBSTR ve REGEXP_REPLACE adlı Oracle SQL fonksiyonlarında kullanılabilen ve regular expression'ın ifade ettiği desenlerin oluşumunu sağlayan ifadeler bulunmaktadır.

| Desen      | Açıklama                                                                                                   |
|------------|------------------------------------------------------------------------------------------------------------|
| ^          | Bir string'in başlangıcını belirtir.                                                                       |
| $          | Bir string'in bitişini belirtir.                                                                           |
| *          | 0 veya daha fazla kez tekrarlama                                                                           |
| +          | 1 veya daha fazla kez tekrarlama                                                                           |
| ?          | 0 veya 1 kez tekrarlama                                                                                    |
| .          |                                                                                                            |
| \|         | Veya anlamı taşır. Alternatif oluşturan bir karakterdir.                                                   |
| \          | Kaçış karakteridir. Özel anlam taşıyan regex metakarakterlerini o anlam dışında kullanmak için kullanılır. |
| [ ]        | İçinde yer alan karakterlerle eşleşme                                                                      |
| [^ ]       | İçinde yer alan karakterlerle eşleşmeme                                                                    |
| ( )        | Grup oluşturur.                                                                                            |
| {m}        | m kez tekrarlama                                                                                           |
| {m,}       | m veya daha fazla kez tekrarlama                                                                           |
| {m,n}      | En az m, en çok n kez tekrarlama                                                                           |
| \n         |                                                                                                            |
| [::]       |                                                                                                            |
| [==]       |                                                                                                            |
| \d         | 0-9 Python'da farklı rakamları da destekliyor. Arapların dilini mesela.                                    |
| \D         | not 0-9                                                                                                    |
| \w         | [a-zA-Z0-9_]                                                                                               |
| \W         | not [a-zA-Z0-9_]                                                                                           |
| \s         |                                                                                                            |
| \S         |                                                                                                            |
| \A         |                                                                                                            |
| \Z         |                                                                                                            |
| *?         |                                                                                                            |
| +?         |                                                                                                            |
| ??         |                                                                                                            |
| {n}?       |                                                                                                            |
| {n,}?      |                                                                                                            |
| {n,m}?     |                                                                                                            |
| [:alnum:]  |                                                                                                            |
| [:alpha:]  |                                                                                                            |
| [:digit:]  |                                                                                                            |
| [:lower:]  |                                                                                                            |
| [:upper:]  |                                                                                                            |
| [:space:]  |                                                                                                            |
| [:punct:]  |                                                                                                            |
| [:xdigit:] |                                                                                                            |
| [:blank:]  |                                                                                                            |
| [:cntrl:]  |                                                                                                            |
| [:graph:]  |                                                                                                            |
| [:print:]  |                                                                                                            |
