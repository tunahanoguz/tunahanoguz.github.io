---
title: "Oracle - ROWNUM ve ROWID"
date: 2025-07-03 20:30:00 +0300
layout: post
categories: oracle
---

`ROWNUM` ve `ROWID` Oracle'da bulunan pseudo kolonlardan biridir. Pseudo kolonlar, tablolarda fiziksel olarak bulunmazlar ancak, çağırıldıklarında tablonun bir kolonu gibi davranış gösterirler.

## `ROWNUM`

`ROWNUM` pseudo kolonu, bir sorgu sonucu getirilen her bir satıra Oracle veritabanının otomatik olarak verdiği bir sıra numarasıdır. 1 ile başlar ve ardışık olarak devam eder. Sorguda yer alan `ORDER BY` ifadesi ile yapılan sıralama, `ROWNUM` değerlerini değiştirmez çünkü `ROWNUM`, Oracle'ın sorgu sonucu gelen kayıtları internal olarak hangi sıra ile çektiğini ifade eder. Oracle'ın verileri çekme sırası birçok farklı durumundan etkilenebilir. Bu sebeple aynı sorgu her çalıştığında bu davranış değişebilir ve bunun sonucunda `ROWNUM` değeri de değişir.

```sql
SELECT ROWNUM, TUTAR
FROM (
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
);
```

| ROWNUM | TUTAR |
| ------ | ----- |
| 1      | 40    |
| 2      | 30    |
| 3      | 10    |
| 4      | 20    |
| 5      | 50    |

<br>

```sql
SELECT ROWNUM, TUTAR
FROM (
	SELECT 40 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 50 AS TUTAR FROM DUAL
)
ORDER BY TUTAR;
```

| ROWNUM | TUTAR |
| ------ | ----- |
| 3      | 10    |
| 4      | 20    |
| 2      | 30    |
| 1      | 40    |
| 5      | 50    |

---

## `ROWID`

- `ROWID` pseudo kolonu, ilgili satırın fiziksel adresi bilgisini içerir. Bir satırın fiziksel adresi, satırın disk üzerindeki yerini gösterir.
- Her tablonun her satırı için mutlaka bir `ROWID` değeri bulunur.
- Satır silinmediği veya taşınmadığı sürece bu değer değişmez.
- `ROWID` ile, ilgili satıra erişim çok hızlıdır çünkü doğrudan fiziksel konuma gidilir.
- `ROWID` değeri her satır için tablo özelinde benzersizdir.
- Genellikle bir `ROWID` değeri veritabanındaki her satır için benzersizdir. Ancak, farklı tablolarda olup da aynı cluster üzerinde birlikte depolanan iki satır, aynı `ROWID` değerine sahip olabilir.
- `ROWID`, tablolar için `primary key` olarak kullanılmamalıdır çünkü kalıcı bir değer değildir. Bir satırın fiziksel adresinin değişmesine sebep olabilecek her işlem bu değerin de değişmesine sebep olabilir. Örneğin, bir tablo veya o tablonun bulunduğu segmentte yapılacak bir move işlemi bu değişime sebep olabilir. Eğer bir satır silinirse, ona ait `ROWID` değeri daha sonra insert edilen yeni bir satıra atanabilir.
- `ROWID`, ilgili satırın lokasyonuna dair aşağıdaki bilgileri içerir:
	- Satırın temsil ettiği `data object`'in numarası 
	- Satırın bulunduğu `datafile`'ın `data block` numarası
	- Satırın bulunduğu `data block` içerisindeki pozisyonu (ilk satırın pozisyonu 0)
	- Satırın bulunduğu `datafile` numarası. İlk datafile için 1'dir. `Datafile`'ın bulunduğu `tablespace` ile ilişkilidir.

```sql
SELECT  ROWID,
	EMPLOYEE_ID,
	FIRST_NAME,
	LAST_NAME
FROM HR.EMPLOYEES
ORDER BY EMPLOYEE_ID;
```

| ROWID              | EMPLOYEE_ID | FIRST_NAME | LAST_NAME |
| ------------------ | ----------- | ---------- | --------- |
| AAAWFBAAAAAAAWsAAA | 100         | Steven     | King      |
| AAAWFBAAAAAAAWsAAB | 101         | Neena      | Yang      |
| AAAWFBAAAAAAAWsAAC | 102         | Lex        | Garcia    |
| AAAWFBAAAAAAAWsAAD | 103         | Alexander  | James     |
| AAAWFBAAAAAAAWsAAE | 104         | Bruce      | Miller    |
