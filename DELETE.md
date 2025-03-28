
# Komenda `DELETE` w MariaDB – Wyjaśnienie i przykłady

Komenda `DELETE` służy do usuwania danych z tabeli. Jest bardzo skuteczna, ale wymaga ostrożności – brak klauzuli `WHERE` może spowodować usunięcie wszystkich danych.

---

## 🔹 Podstawowa składnia

```sql
DELETE FROM nazwa_tabeli
WHERE warunek;
```

---

## 🛑 UWAGA

Bez klauzuli `WHERE` usuniesz **wszystkie** wiersze z tabeli!

```sql
DELETE FROM customers;
-- Usunie wszystkich klientów
```

---

## 🔸 Przykłady na Twoich tabelach

### ✅ 1. Usuń klienta o konkretnym ID

```sql
DELETE FROM customers
WHERE customer_id = 5;
```

---

### ✅ 2. Usuń wszystkie produkty nieaktywne

```sql
DELETE FROM products
WHERE active = FALSE;
```

---

### ✅ 3. Usuń zamówienia o statusie 'cancelled'

```sql
DELETE FROM orders
WHERE status = 'cancelled';
```

---

### ✅ 4. Usuń rekordy magazynowe o zerowym stanie

```sql
DELETE FROM inventory
WHERE quantity = 0;
```

---

## 🔹 DELETE z LIMIT

```sql
DELETE FROM products
WHERE active = FALSE
LIMIT 3;
```

Usuwa tylko 3 pierwsze pasujące rekordy.

---

## 🔹 DELETE z JOIN (MariaDB)

MariaDB pozwala usuwać dane z jednej tabeli na podstawie połączenia z inną tabelą.

### ✅ Przykład: Usuń klientów, którzy nie mają adresu

```sql
DELETE c
FROM customers c
LEFT JOIN addresses a ON c.customer_id = a.customer_id
WHERE a.customer_id IS NULL;
```

---

## 🔹 DELETE vs TRUNCATE

| Operacja  | Co robi?                     | Kiedy używać?                       |
|-----------|------------------------------|-------------------------------------|
| `DELETE`  | Usuwa wybrane wiersze        | Gdy chcesz usunąć konkretne dane    |
| `TRUNCATE`| Czyści całą tabelę błyskawicznie | Gdy chcesz opróżnić tabelę całkowicie |

---

