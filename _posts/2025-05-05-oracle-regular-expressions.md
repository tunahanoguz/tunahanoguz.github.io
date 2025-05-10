---
title:  "Oracle - Regular Expressions"
layout: post
categories: oracle
---

Regular expression (düzenli ifade), bir metindeki eşleşme desenini ifade eden karakter dizisidir. Regex ve regexp olarak kısaltılabilir. Regular expression, ifade ettiği desen ile genel olarak bir metin üzerinde arama yapmak, eşleşen kısmı metinden elde etmek ve düzenlemek için kullanılır.

Birçok yazılım dilinde ve o yazılım dilinde kullanılan modül/paket/kütüphanelerde regular expression için özel fonksiyonlar bulunur. Bu fonksiyonların isimleri, aldıkları parametreler ve regular expression desenindeki standartlar her yazılım dili/modül/paket/kütüphanede farklılaşabilir. Örneğin, positive lookahead ve negative lookahead gibi yapılar şimdilik Oracle üzerinde çalışmıyor. `[:KARAKTERSINIFIADI:]` yapısındaki POSIX karakter sınıfları Oracle'da kullanılabilirken, Python'ın yerleşik regular expression modülü olan `re`'de kullanılamaz. Kullanabilmek için `regex` modülünü yüklemek gerekir. Ben bu yazıda regular expression konusunu Oracle odaklı olarak işleyeceğim.

---

## İçindekiler
1. [Desenler ve Açıklamaları](#desenler-ve-aciklamalari)
2. [Eşleşme Modları](#eslesme-modlari)
3. [Desenler ve Eşleşme Modları İçin Örnekler](#desenler-ve-eslesme-modlari-icin-ornekler)
4. [Oracle Regular Expression Fonksiyonları](#oracle-regular-expression-fonksiyonlari)
    1. [REGEXP_INSTR](#REGEXP_INSTR)
    2. [REGEXP_SUBSTR](#REGEXP_SUBSTR)
    3. [REGEXP_REPLACE](#REGEXP_REPLACE)
    4. [REGEXP_COUNT](#REGEXP_COUNT)
    5. [REGEXP_LIKE](#REGEXP_LIKE)

---

## 1. Desenler ve Açıklamaları {#desenler-ve-aciklamalari}

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

---

## 2. Eşleşme Modları {#eslesme-modlari}

Aşağıdaki tabloda yine `REGEXP_INSTR`, `REGEXP_COUNT`, `REGEXP_LIKE`, `REGEXP_SUBSTR` ve `REGEXP_REPLACE` adlı Oracle SQL fonksiyonlarında eşleşme davranışını düzenlemek için kullanılan değerler yer almaktadır.

| Eşleşme Modu | Açıklama                                                                                                                              |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------|
| c            | Case-sensitive eşleşme gerçekleşmesini sağlar.                                                                                        |
| i            | Case-insensitive eşleşme gerçekleşmesini sağlar.                                                                                      |
| n            | `.` karakterinin `newline` karakteri ile eşleşmesini sağlar.                                                                          |
| m            | Eşleşme modunu `multiline mode` olarak düzenler. Bu mod pasifken `^` tüm metnin başını, `$` tüm metnin sonunu, aktifken `^` her satırın başını, `$` her satırın sonunu ifade eder. |
| x            | Desendeki boşlukları ve yorumları yok sayar. Yorumlar `#` ile başlar ve satır sonunda sona erer. Yorumlar sadece bu modda geçerlidir. |

---

## 3. Desenler ve Eşleşme Modları İçin Örnekler {#desenler-ve-eslesme-modlari-icin-ornekler}

Aşağıdaki tabloda üstteki iki tabloda açıklamaları yer alan desen ve eşleşme modları için örnekler yer almaktadır.

| String              | Desen                               | Mod | Eşleşti mi? |
|---------------------|-------------------------------------|-----|-------------|
| John                | `^J`                                | -   | 🟢           |
| John                | `n$`                                | -   | 🟢           |
| John                | `^Jo*hn$`                           | -   | 🟢           |
| Joohn               | `^Jo*hn$`                           | -   | 🟢           |
| Jhn                 | `^Jo*hn$`                           | -   | 🟢           |
| John                | `^Jo+hn$`                           | -   | 🟢           |
| Joohn               | `^Jo+hn$`                           | -   | 🟢           |
| Jhn                 | `^Jo+hn$`                           | -   | 🔴           |
| John                | `^Jo?hn$`                           | -   | 🟢           |
| Joohn               | `^Jo?hn$`                           | -   | 🔴           |
| Jhn                 | `^Jo?hn$`                           | -   | 🟢           |
| John                | `^J.hn$`                            | -   | 🟢           |
| John                | `^J...$`                            | -   | 🟢           |
| John                | `^J.*$`                             | -   | 🔴           |
| John                | `^J.*n$`                            | -   | 🟢           |
| John                | `^.*$`                              | -   | 🟢           |
| John                | ```^Jo|ahn$```                      | -   | 🟢           |
| Jahn                | ```^Jo|ahn$```                      | -   | 🟢           |
| Jehn                | ```^Jo|ahn$```                      | -   | 🔴           |
| J*hn                | ```^J\*hn$```                       | -   | 🟢           |
| Jo+n                | ```^Jo\+n$```                       | -   | 🟢           |
| John                | ```^J[oa]hn$```                     | -   | 🟢           |
| Jahn                | ```^J[oa]hn$```                     | -   | 🟢           |
| Jehn                | ```^J[oa]hn$```                     | -   | 🔴           |
| John                | ```^[A-Z]ohn$```                    | -   | 🟢           |
| Sohn                | ```^[A-Z]ohn$```                    | -   | 🟢           |
| A9                  | ```^[A-Z][0-9]$```                  | -   | 🟢           |
| a9                  | ```^[A-Z][0-9]$```                  | -   | 🔴           |
| A9                  | ```^[^A-Z][0-9]$```                 | -   | 🔴           |
| a9                  | ```^[^A-Z][0-9]$```                 | -   | 🟢           |
| James               | ```^J(ame|one)s$```                 | -   | 🟢           |
| Jones               | ```^J(ame|one)s$```                 | -   | 🟢           |
| Jones               | ```^J(ame|one)s$```                 | -   | 🟢           |
| Jonas               | ```^J(ame|one)s$```                 | -   | 🔴           |
| Joohn               | ```^Jo{2}hn$```                     | -   | 🟢           |
| John                | ```^Jo{2}hn$```                     | -   | 🔴           |
| Jooohn              | ```^Jo{2}hn$```                     | -   | 🔴           |
| Joohn               | ```^Jo{2,}hn$```                    | -   | 🟢           |
| Jooohn              | ```^Jo{2,}hn$```                    | -   | 🟢           |
| John                | ```^Jo{2,}hn$```                    | -   | 🔴           |
| Joohn               | ```^Jo{2,4}hn$```                   | -   | 🟢           |
| Jooohn              | ```^Jo{2,4}hn$```                   | -   | 🟢           |
| Joooohn             | ```^Jo{2,4}hn$```                   | -   | 🟢           |
| John                | ```^Jo{2,4}hn$```                   | -   | 🔴           |
| Jooooohn            | ```^Jo{2,4}hn$```                   | -   | 🔴           |
| John James Jennifer | ```^([A-Z])ohn \1ames \1ennifer$``` | -   | 🟢           |
| John James Doe      | ```^([A-Z])ohn \1ames \1oe$```      | -   | 🔴           |
| 9                   | ```^\d$```                          | -   | 🟢           |
| 10                  | ```^\d{2}$```                       | -   | 🟢           |
| A9                  | ```^[A-Z]\d$```                     | -   | 🟢           |
| A9                  | ```^\D\d$```                        | -   | 🟢           |
| a9                  | ```^\D\d$```                        | -   | 🟢           |
| _9                  | ```^\D\d$```                        | -   | 🟢           |
| 19                  | ```^\D\d$```                        | -   | 🔴           |
| A                   | ```\w```                            | -   | 🟢           |
| a                   | ```\w```                            | -   | 🟢           |
| 9                   | ```\w```                            | -   | 🟢           |
| _                   | ```\w```                            | -   | 🟢           |
| ?                   | ```\w```                            | -   | 🔴           |
| *                   | ```\w```                            | -   | 🔴           |
| A                   | ```\W```                            | -   | 🔴           |
| a                   | ```\W```                            | -   | 🔴           |
| 9                   | ```\W```                            | -   | 🔴           |
| _                   | ```\W```                            | -   | 🔴           |
| ?                   | ```\W```                            | -   | 🟢           |
| *                   | ```\W```                            | -   | 🟢           |
| *1                  | ```\W\w```                          | -   | 🟢           |
| John Doe            | ```^John\sDoe$```                   | -   | 🟢           |
| John Doe            | ```^\S{4}\s\S{3}$```                | -   | 🟢           |
| John                | `\AJ`                               | -   | 🟢           |
| John                | `n\Z`                               | -   | 🟢           |

---

## 4. Oracle Regular Expression Fonksiyonları {#oracle-regular-expression-fonksiyonlari}

### 4.1 REGEXP_INSTR {#REGEXP_INSTR}

- Bir desenin bir metin içerisindeki eşleşmesinin konumunu döner.
- Hiç eşleşme olmazsa 0 dönecektir.
- İki adet zorunlu, beş adet opsiyonel olmak üzere toplam yedi adet parametreye sahiptir.

{% highlight %}
REGEXP_INSTR(metin, desen, [baslama_konumu], [kacinci_eslesme], [donus_modu], [eslesme_modu], [alt_ifade])
{% endhighlight %}

1. ```metin```: *zorunlu* Desenin üzerinde çalışacağı string ifadedir.
2. ```desen```: *zorunlu* Regular expression
3. ```baslama_konumu```: *[opsiyonel]* Metnin kaçıncı karakterinden itibaren eşleşme aranacağını ifade eder.
4. ```kacinci_eslesme```: *[opsiyonel]*
5. ```donus_modu```: *[opsiyonel]*
6. ```eslesme_modu```: *[opsiyonel]*
7. ```alt_ifade```: *[opsiyonel]*

### 4.2 REGEXP_SUBSTR {#REGEXP_SUBSTR}

- Bir metnin desenin eşleştiği kısmını döner.
- Hiç eşleşme olmazsa NULL dönecektir.
- İki adet zorunlu, dört adet opsiyonel olmak üzere toplam altı adet parametreye sahiptir.

```REGEXP_SUBSTR(metin, desen, [baslama_konumu], [kacinci_eslesme], [eslesme_modu], [alt_ifade])```

1. ```metin```: *zorunlu* Desenin üzerinde çalışacağı string ifadedir.
2. ```desen```: *zorunlu* Regular expression
3. ```baslama_konumu```: *[opsiyonel]* Metnin kaçıncı karakterinden itibaren eşleşme aranacağını ifade eder.
4. ```kacinci_eslesme```: *[opsiyonel]*
5. ```eslesme_modu```: *[opsiyonel]*
6. ```alt_ifade```: *[opsiyonel]*

### 4.3 REGEXP_REPLACE {#REGEXP_REPLACE}

- Bir metnin desenin eşleştiği kısmını başka bir metin ile değiştirir ve oluşan yeni metni döner.
- Hiç eşleşme olmazsa herhangi bir değiştirme işlemi olmaz ve metnin ilk hali döner.
- İki adet zorunlu, dört adet opsiyonel parametreye sahiptir.

```REGEXP_REPLACE(metin, desen, [degistirilecek_metin], [baslama_konumu], [kacinci_eslesme], [eslesme_modu])```

1. ```metin```: *zorunlu* Desenin üzerinde çalışacağı string ifadedir.
2. ```desen```: *zorunlu* Regular expression
3. ```degistirilecek_metin```: *[opsiyonel]*
4. ```baslama_konumu```: *[opsiyonel]* Metnin kaçıncı karakterinden itibaren eşleşme aranacağını ifade eder.
5. ```kacinci_eslesme```: *[opsiyonel]*
6. ```eslesme_modu```: *[opsiyonel]*

### 4.4 REGEXP_COUNT {#REGEXP_COUNT}

- Bir desenin bir metinde kaç defa eşleşme yakaladığını döner.
- İki adet zorunlu, iki adet opsiyonal parametreye sahiptir.

```REGEXP_COUNT(metin, desen, [baslama_konumu], [eslesme_modu])```

1. ```metin```: *zorunlu* Desenin üzerinde çalışacağı string ifadedir.
2. ```desen```: *zorunlu* Regular expression
3. ```baslama_konumu```: *[opsiyonel]* Metnin kaçıncı karakterinden itibaren eşleşme aranacağını ifade eder.
4. ```eslesme_modu```: *[opsiyonel]*

### 4.5 REGEXP_LIKE {#REGEXP_LIKE}

- Bir desenin bir metinde eşleşme yakalayıp yakalayamadığını döner.
- Dönüş değeri TRUE veya FALSE olabilir.
- İki adet zorunlu, bir adet opsiyonel parametre sahiptir.

```REGEXP_LIKE(metin, desen, [eslesme_modu])```

1. ```metin```: *zorunlu* Desenin üzerinde çalışacağı string ifadedir.
2. ```desen```: *zorunlu* Regular expression
3. ```eslesme_modu```: *[opsiyonel]*
