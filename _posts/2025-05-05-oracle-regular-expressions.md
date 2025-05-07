---
title:  "Oracle - Regular Expressions"
layout: post
categories: oracle
---

Regular expression (düzenli ifade), bir metindeki eşleşme desenini ifade eden karakter dizisidir. Regex ve regexp olarak kısaltılabilir. Regular expression, ifade ettiği desen ile genel olarak bir metin üzerinde arama yapmak, eşleşen kısmı metinden elde etmek ve düzenlemek için kullanılır.

Birçok yazılım dilinde ve o yazılım dilinde kullanılan modül/paket/kütüphanelerde regular expression için özel fonksiyonlar bulunur. Bu fonksiyonların isimleri, aldıkları parametreler ve regular expression desenindeki standartlar her yazılım dili/modül/paket/kütüphanede farklılaşabilir. Örneğin, positive lookahead ve negative lookahead gibi yapılar şimdilik Oracle üzerinde çalışmıyor. `[:KARAKTERSINIFIADI:]` yapısındaki POSIX karakter sınıfları Oracle'da kullanılabilirken, Python'ın yerleşik regular expression modülü olan `re`'de kullanılamaz. Kullanabilmek için `regex` modülünü yüklemek gerekir. Ben bu yazıda regular expression konusunu Oracle odaklı olarak işleyeceğim.

Aşağıdaki tabloda `REGEXP_INSTR`, `REGEXP_COUNT`, `REGEXP_LIKE`, `REGEXP_SUBSTR` ve `REGEXP_REPLACE` adlı Oracle SQL fonksiyonlarında kullanılabilen ve regular expression'ın ifade ettiği desenlerin oluşumunu sağlayan ifadeler bulunmaktadır.

| Desen      | Açıklama                                                                                                        |
|------------|-----------------------------------------------------------------------------------------------------------------|
| ^          | Bir string'in başlangıcını belirtir. Eğer eşleşme modu `m` ise her satırın başlangıcını belirtir.               |
| $          | Bir string'in bitişini belirtir. Eğer eşleşme modu `m` ise her satırın bitişini belirtir.                       |
| *          | 0 veya daha fazla kez tekrarlama                                                                                |
| +          | 1 veya daha fazla kez tekrarlama                                                                                |
| ?          | 0 veya 1 kez tekrarlama                                                                                         |
| .          | `NULL` dışında tüm karakterler ile eşleşir.                                                                     |
| \|         | Veya anlamı taşır. Alternatif oluşturan bir karakterdir.                                                        |
| \          | Kaçış karakteridir. Özel anlam taşıyan regex metakarakterlerini o anlam dışında kullanmak için kullanılır.      |
| [ ]        | İçinde yer alan karakterlerle eşleşme                                                                           |
| [^ ]       | İçinde yer alan karakterlerle eşleşmeme                                                                         |
| ( )        | Grup oluşturur.                                                                                                 |
| {m}        | `m` kez tekrarlama                                                                                              |
| {m,}       | `m` veya daha fazla kez tekrarlama                                                                              |
| {m,n}      | En az `m`, en çok `n` kez tekrarlama                                                                            |
| \n         | Kendisinden önce `( )` ile oluşturulan grupların aynı ifadeyi tekrar yazmadan tekrar kullanılmasını sağlar.     |
| [::]       | POSIX karakter sınıfı ile eşleşir. Tablonun son satırlarında tüm POSIX karakter sınıflarının açıklamaları var.  |
| [==]       | Bir POSIX özelliği olup, eşittir karakterleri arasında konan harfin farklı aksanlarıyla da eşleme sağlar.       |
| \d         | 0-9 arasındaki rakamlar ile eşleşir. (Python'da farklı dillerdeki rakamları da destekliyor.)                    |
| \D         | 0-9 arasındaki rakamlar hariç her karakter ile eşleşir.                                                         |
| \w         | Harfler, 0-9 arasındaki rakamlar ve alt çizgi ile eşleşir. `[a-zA-Z0-9_]`                                       |
| \W         | Harfler, 0-9 arasındaki rakamlar ve alt çizgi hariç her karakter ile eşleşir.                                   |
| \s         | Boşluk karakteri ile eşleşir.                                                                                   |
| \S         | Boşluk karakteri dışındaki her karakter ile eşleşir.                                                            |
| \A         | Bir string'in başlangıcını belirtir. Eşleşme modu `m` olsa bile sadece ilk satırın başlangıcını belirtir.       |
| \Z         | Bir string'in bitişini belirtir. Eşleşme modu `m` olsa bile sadece ilk satırın bitişini belirtir.               |
| *?         | `*` karakteri tek başına 0 veya daha fazla kez tekrarlama arar ve greedy (açgözlü) eşleşme sağlar. Yani mümkün olan en geniş eşleşmeyi arar. `*?` ise, `*` karakterinin anlamını korumakla birlikte, non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| +?         | `+` karakteri tek başına 1 veya daha fazla tekrarlama arar ve greedy (açgözlü) bir anlayışla eşleşme sağlar. `+?` ise, `+` karakterinin anlamını korumakla birlikte, non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| ??         | `?` karakteri tek başına 0 veya 1 kez tekrarlama arar ve greedy (açgözlü) bir anlayışla eşleşme sağlar. `??` ise, `?` karakterinin anlamını korumakla birlikte,  non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| {m}?       | `{m}` deseni tek başına `m` kez tekrarlama arar ve greedy (açgözlü) bir anlayışla eşleşme sağlar. `{m}?` ise, `{m}` deseninin anlamını korumakla birlikte,  non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| {m,}?      | `{m,}` deseni tek başına `m` veya daha fazla kez tekrarlama arar ve greedy (açgözlü) bir anlayışla eşleşme sağlar. `{m,}?` ise, `{m,}` deseninin anlamını korumakla birlikte,  non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| {m,n}?     | `{m,n}` deseni tek başına en az `m`, en çok `n` kez tekrarlama arar ve greedy (açgözlü) bir anlayışla eşleşme sağlar. `{m,n}?` ise, `{m,n}` deseninin anlamını korumakla birlikte,  non-greedy veya lazy olarak ifade edilen bir anlayışla eşleşme sağlar. Bu da mümkün olan en dar eşleşmenin aranacağı anlamına gelir. |
| [:alnum:]  | Alfabetik bir karakter veya 0-9 arasındaki bir rakam ile eşleşir. `[a-zA-Z0-9]`                                 |
| [:alpha:]  | Alfabetik bir karakter ile eşleşir. `[a-zA-Z]`                                                                  |
| [:digit:]  | 0-9 arasındaki bir rakam ile eşleşir. `[0-9]`                                                                   |
| [:lower:]  | Küçük alfabetik bir karakter ile eşleşir. `[a-z]`                                                               |
| [:upper:]  | Büyük alfabetik bir karakter ile eşleşir. `[A-Z]`                                                               |
| [:space:]  | `horizontal tab`, `newline (line feed)`, `vertical tab`, `form feed (new page)`, `carriage return` ve `space` karakterlerinden biriyle eşleşir.   |
| [:punct:]  | Bir noktalama işareti ile eşleşir. <br> ```! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~```   |
| [:xdigit:] | Hexadecimal (on altılı) sayı sisteminde yer alan bir sembol ile eşleşir. <br> `0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f` |
| [:blank:]  | Boşluk veya tab karakteri ile eşleşir.                                                                          |
| [:cntrl:]  | ASCII kontrol karakteri ile eşleşir. Bu karakterler, 000-037 ve 177 oktal kodlara sahip ASCII karakterleridir.  |
| [:graph:]  | `[:alnum:]` ve `[:punct:]` karakter sınıflarının eşleştiği bir karakter ile eşleşir.                            |
| [:print:]  | `[:alnum:]` ve `[:punct:]` karakter sınıflarının eşleştiği bir karakter ve boşluk karakteri ile eşleşir.        |
