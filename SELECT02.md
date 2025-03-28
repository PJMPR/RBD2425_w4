
# `SELECT` z klauzulą `HAVING` w MariaDB – Przykłady z funkcjami agregującymi

## 🔹 Co to jest `HAVING`?

`HAVING` służy do filtrowania wyników **po agregacji**, czyli po użyciu funkcji takich jak `SUM`, `AVG`, `COUNT`, itd.

| Klauzula | Kiedy działa? | Do czego służy?                     |
|----------|----------------|-------------------------------------|
| `WHERE`  | przed agregacją | Filtruje **pojedyncze wiersze**    |
| `HAVING` | po agregacji    | Filtruje **zgrupowane wyniki**     |

---

## 🔹 Składnia

```sql
SELECT kolumny_agregujące
FROM tabela
GROUP BY kolumny_grupujące
HAVING warunek_na_agregatach;
```

---

## 🔸 Przykłady z tabel

### ✅ 1. Klienci z więcej niż jednym zamówieniem

```sql
SELECT customer_id, COUNT(*) AS liczba_zamowien
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

---

### ✅ 2. Produkty zamówione w sumie więcej niż 10 razy

```sql
SELECT product_id, SUM(quantity) AS laczna_ilosc
FROM order_items
GROUP BY product_id
HAVING SUM(quantity) > 10;
```

---

## 🔹 Funkcje agregujące i `HAVING` – Przykłady

### ✅ `AVG()` – Średnia wartość zamówienia powyżej 1000 zł

```sql
SELECT customer_id, AVG(quantity * price) AS srednia_wartosc
FROM order_items_view
GROUP BY customer_id
HAVING AVG(quantity * price) > 1000;
```

---

### ✅ `SUM()` – Produkty o sprzedaży powyżej 5000 zł

```sql
SELECT product_id, SUM(quantity * price) AS przychod
FROM order_items_view
GROUP BY product_id
HAVING SUM(quantity * price) > 5000;
```

---

### ✅ `MIN()` – Najtańsze zamówienie klienta co najmniej 100 zł

```sql
SELECT customer_id, MIN(quantity * price) AS minimalne_zamowienie
FROM order_items_view
GROUP BY customer_id
HAVING MIN(quantity * price) >= 100;
```

---

### ✅ `MAX()` – Największe pojedyncze zamówienie produktu > 10 sztuk

```sql
SELECT product_id, MAX(quantity) AS maks_ilosc
FROM order_items
GROUP BY product_id
HAVING MAX(quantity) > 10;
```

---

### ✅ `COUNT(DISTINCT)` – Klienci, którzy kupili więcej niż 3 różne produkty

```sql
SELECT customer_id, COUNT(DISTINCT product_id) AS unikalne_produkty
FROM order_items
GROUP BY customer_id
HAVING COUNT(DISTINCT product_id) > 3;
```

---

## 🔹 `HAVING` bez `GROUP BY`

```sql
SELECT COUNT(*) AS liczba_klientow
FROM customers
HAVING COUNT(*) > 10;
```

---

## 🔹 `WHERE` + `HAVING` razem

### ✅ Tylko aktywne produkty (`WHERE`), które sprzedały się w ilości powyżej 20 sztuk (`HAVING`)

```sql
SELECT product_id, SUM(quantity) AS laczna_sprzedaz
FROM order_items
WHERE product_id IN (
    SELECT product_id FROM products WHERE active = TRUE
)
GROUP BY product_id
HAVING SUM(quantity) > 20;
```

---
