# Komenda `SELECT` w MariaDB – Przykłady podstawowego użycia z `WHERE`, `ORDER BY` i `LIMIT`

## 🔹 Podstawowa składnia `SELECT` z `WHERE`

```sql
SELECT kolumna1, kolumna2, ...
FROM nazwa_tabeli
WHERE warunek;
```

---

## 🔸 PRZYKŁADY DLA TABEL

### ✅ 1. Wyszukiwanie klienta po nazwisku (`customers`)

```sql
SELECT customer_id, first_name, last_name, email
FROM customers
WHERE last_name = 'Nowak';
```

---

### ✅ 2. Sprawdzenie klientów z określonym adresem e-mail

```sql
SELECT *
FROM customers
WHERE email = 'anna.nowak@example.com';
```

---

### ✅ 3. Produkty, które są aktywne (`products`)

```sql
SELECT name, price
FROM products
WHERE active = TRUE;
```

---

### ✅ 4. Produkty tańsze niż 1000 zł

```sql
SELECT name, price
FROM products
WHERE price < 1000;
```

---

### ✅ 5. Stan magazynowy dla wybranego produktu (`inventory`)

```sql
SELECT *
FROM inventory
WHERE product_id = 1;
```

---

### ✅ 6. Wszystkie zamówienia danego klienta (`orders`)

```sql
SELECT order_id, order_date, status
FROM orders
WHERE customer_id = 1;
```

---

### ✅ 7. Pozycje konkretnego zamówienia (`order_items`)

```sql
SELECT product_id, quantity
FROM order_items
WHERE order_id = 1;
```

---

### ✅ 8. Adresy w wybranym mieście (`addresses`)

```sql
SELECT street, zip_code
FROM addresses
WHERE city = 'Warszawa';
```

---

## 🔹 Operatory w `WHERE`

| Operator | Znaczenie                | Przykład                          |
|----------|--------------------------|-----------------------------------|
| `=`      | równa się                | `WHERE country = 'Polska'`        |
| `!=` / `<>` | różne                  | `WHERE city <> 'Warszawa'`        |
| `<`, `<=`, `>`, `>=` | porównania    | `WHERE price > 2000`              |
| `LIKE`   | dopasowanie wzorca       | `WHERE email LIKE '%@gmail.com'` |
| `IN (...)` | zawiera się w zbiorze  | `WHERE status IN ('new', 'shipped')` |
| `IS NULL`, `IS NOT NULL` | null     | `WHERE zip_code IS NOT NULL`      |

---

## 🔹 Użycie `ORDER BY`

```sql
SELECT name, price
FROM products
WHERE active = TRUE
ORDER BY price DESC;
```
- Sortuje wyniki według ceny malejąco (`DESC`).
- Można użyć `ASC` (domyślnie) do sortowania rosnąco.

---

## 🔹 Użycie `LIMIT`

```sql
SELECT name, price
FROM products
WHERE active = TRUE
ORDER BY price ASC
LIMIT 5;
```

- Zwraca **tylko 5 pierwszych wyników**.
- Możesz też dodać OFFSET: `LIMIT 5 OFFSET 10` (np. do paginacji).

---

