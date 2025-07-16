---
title:  "Oracle - Aggregate Function vs Analytic Function"
date: 2025-06-06 10:30:00 +0300
layout: post
categories: oracle
---

`Aggregate function`, bir veya birden fazla satırda yer alan bir dizi değer için hesaplama yapar ve tek bir satır olarak bu hesaplamanın sonucunu döner. `GROUP BY` ifadesi ile kullanıldığında her bir grup için veri tek satıra indirgenir/özetlenir, aksi durumda gruplama yapılmadan tüm satırlar tek satıra indirgenir/özetlenir. Genellikle toplama, ortalama alma, kayıt sayısını tespit etme, maksimum ve minimum değerleri bulma gibi amaçlar için kullanılır. Yaygın olarak kullanılan bazı fonksiyonlar: `SUM`, `AVG`, `COUNT`, `MAX`, `MIN`

`Analytic function` da tıpkı `aggregate function` gibi bir veya birden fazla satırda yer alan bir dizi değer için hesaplama yapar ancak bu satırları tek bir satıra indirgeyen bir davranış sergilemez. Dönüş değeri her bir satır için ayrı ayrı gösterilir. Yaygın olarak kullanılan bazı fonksiyonlar: `SUM`, `AVG`, `FIRST_VALUE`, `LAST_VALUE`, `NTH_VALUE`, `LAG`, `LEAD`

`SUM` ve `AVG` gibi fonksiyonlar hem `aggregate function` hem de `analytic function` olarak kullanılabilir. Ayrışma syntax üzerinde oluşur:

| Aggregate Function | Analytic Function                                           |
| ------------------ | ----------------------------------------------------------- |
| `SUM(expression)`  | `SUM([ DISTINCT \| ALL ] expression) OVER(analytic_clause)` |
| `AVG(expression)`  | `AVG([ DISTINCT \| ALL ] expression) OVER(analytic_clause)` |

---

Aşağıda aggregate ve analytic function için örnekler bulunmaktadır.

| BOLGE   | SEHIR     | NUFUS      |
| ------- | --------- | ---------- |
| Marmara | İstanbul  | 16.000.000 |
| Marmara | Bursa     | 3.200.000  |
| Marmara | Çanakkale | 600.000    |
| Ege     | İzmir     | 5.000.000  |
| Ege     | Muğla     | 1.100.000  |
| Ege     | Aydın     | 1.200.000  |

```sql
SELECT SUM(NUFUS)
FROM SEHIRLER
```

| SUM(NUFUS) |
| ---------- |
| 27.100.000 |

```sql
SELECT BOLGE, SUM(NUFUS)
FROM SEHIRLER
GROUP BY BOLGE
ORDER BY BOLGE
```

| BOLGE   | SUM(NUFUS) |
| ------- | ---------- |
| Ege     | 7.300.000  |
| Marmara | 19.800.000 |

```sql
SELECT BOLGE, SEHIR, NUFUS, SUM(NUFUS) OVER(PARTITION BY BOLGE)
FROM SEHIRLER
ORDER BY BOLGE, SEHIR
```

| BOLGE   | SEHIR     | NUFUS      | SUM(NUFUS) OVER... |
| ------- | --------- | ---------- | ------------------ |
| Ege     | Aydın     | 1.200.000  | 7.300.000          |
| Ege     | İzmir     | 5.000.000  | 7.300.000          |
| Ege     | Muğla     | 1.100.000  | 7.300.000          |
| Marmara | Bursa     | 3.200.000  | 19.800.000         |
| Marmara | Çanakkale | 600.000    | 19.800.000         |
| Marmara | İstanbul  | 16.000.000 | 19.800.000         |
