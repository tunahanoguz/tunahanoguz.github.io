---
title: "Oracle - ANY, SOME ve ALL Operatörleri"
date: 2025-06-28 16:30:00 +0300
layout: post
categories: oracle
---

| Kullanım                     | Eşdeğeri                                                |
| ---------------------------- | ------------------------------------------------------- |
| `expression = ANY(x, y, z)`  | `expression = x OR expression = y OR expression = z`    |
| `expression != ANY(x, y, z)` | `expression != x OR expression != y OR expression != z` |
| `expression > ANY(x, y, z)`  | `expression > x OR expression > y OR expression > z`    |
| `expression >= ANY(x, y, z)` | `expression >= x OR expression >= y OR expression >= z` |
| `expression < ANY(x, y, z)`  | `expression < x OR expression < y OR expression < z`    |
| `expression <= ANY(x, y, z)` | `expression <= x OR expression <= y OR expression <= z` |

<br>

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR = ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR = 20 OR TUTAR = 30 OR TUTAR = 40;
```

| TUTAR |
| ----- |
| 20    |
| 30    |

---

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR != ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR != 20 OR TUTAR != 30 OR TUTAR != 40;
```

| TUTAR |
| ----- |
| 10    |
| 20    |
| 30    |

---

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR > ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR > 20 OR TUTAR > 30 OR TUTAR > 40;
```

| TUTAR |
| ----- |
| 30    |

---

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR >= ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR >= 20 OR TUTAR >= 30 OR TUTAR >= 40;
```

| TUTAR |
| ----- |
| 20    |
| 30    |

---

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR < ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR < 20 OR TUTAR < 30 OR TUTAR < 40;
```

| TUTAR |
| ----- |
| 10    |
| 20    |
| 30    |

---

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR <= ANY(20, 30, 40);
```

```sql
SELECT *
FROM (
	SELECT 10 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 20 AS TUTAR FROM DUAL
	UNION ALL
	SELECT 30 AS TUTAR FROM DUAL
)
WHERE TUTAR <= 20 OR TUTAR <= 30 OR TUTAR <= 40;
```

| TUTAR |
| ----- |
| 10    |
| 20    |
| 30    |
