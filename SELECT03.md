
# JOIN-y w MariaDB – Rodzaje i użycie aliasów

## 🔹 Co to jest JOIN?

JOIN służy do łączenia danych z dwóch lub więcej tabel na podstawie relacji między kolumnami.

---

## 🔸 Rodzaje JOIN-ów

| JOIN            | Co zwraca? |
|-----------------|------------|
| `INNER JOIN`    | Tylko pasujące wiersze w obu tabelach |
| `LEFT JOIN`     | Wszystkie z lewej + dopasowane z prawej |
| `RIGHT JOIN`    | Wszystkie z prawej + dopasowane z lewej |
| `FULL OUTER JOIN` | Wszystkie z obu tabel, nawet jak brak dopasowania |
| `JOIN` (domyślny) | To samo co `INNER JOIN` |

---

## 🔹 Składnia ogólna

```sql
SELECT kolumny
FROM tabela1
JOIN tabela2 ON tabela1.klucz = tabela2.klucz;
```

---

## 🔹 Aliasowanie tabel

Alias to tymczasowa, skrócona nazwa nadana tabeli w zapytaniu SQL.

```sql
SELECT * FROM customers AS c;
```

Można też bez `AS`:

```sql
SELECT * FROM customers c;
```

---

## 🔸 Przykłady z aliasami i JOIN-ami

### ✅ 1. INNER JOIN – zamówienia z klientami

```sql
SELECT o.order_id, c.first_name, c.last_name
FROM orders AS o
INNER JOIN customers AS c ON o.customer_id = c.customer_id;
```

---

### ✅ 2. LEFT JOIN – wszystkie zamówienia + dane klientów (mogą być NULL)

```sql
SELECT o.order_id, c.first_name
FROM orders o
LEFT JOIN customers c ON o.customer_id = c.customer_id;
```

---

### ✅ 3. RIGHT JOIN – wszyscy klienci + ich zamówienia (mogą być NULL)

```sql
SELECT o.order_id, c.first_name
FROM orders o
RIGHT JOIN customers c ON o.customer_id = c.customer_id;
```

---

### ✅ 4. FULL OUTER JOIN (symulacja w MariaDB)

```sql
SELECT *
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id

UNION

SELECT *
FROM customers c
RIGHT JOIN orders o ON c.customer_id = o.customer_id;
```

---

### ✅ 5. JOIN domyślny = INNER JOIN

```sql
SELECT o.order_id, c.first_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id;
```

---

### ✅ 6. JOIN z aliasami dla 3 tabel: order_items, orders, products

```sql
SELECT o.order_id, p.name, oi.quantity
FROM order_items oi
LEFT JOIN orders o ON oi.order_id = o.order_id
LEFT JOIN products p ON oi.product_id = p.product_id;
```

---

## ✅ Korzyści z użycia aliasów

- Skracają zapytania
- Ułatwiają czytelność
- Są niezbędne przy wielu tabelach lub kolumnach o tych samych nazwach

---
