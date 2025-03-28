# Przykładowe zadania SQL – Łączenie JOIN, WHERE, HAVING, aliasów i agregacji

Poniżej znajdują się praktyczne zadania SQL, które łączą różne elementy składni SQL, m.in.:
- `JOIN` i aliasy tabel
- `GROUP BY` + funkcje agregujące (`COUNT`, `SUM`)
- `HAVING`, `WHERE`
- `ORDER BY`, `LIMIT`

---

## 🧩 Zadanie 1: Klienci z więcej niż 2 zamówieniami

### 🎯 Cel:
Wyświetl `customer_id`, `first_name`, `last_name` oraz liczbę zamówień dla klientów, którzy złożyli więcej niż 2 zamówienia. Posortuj wynik od największej liczby zamówień i pokaż tylko 10 wyników.

### ✅ Zapytanie:

```sql
SELECT c.customer_id, c.first_name, c.last_name, COUNT(o.order_id) AS liczba_zamowien
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id
HAVING COUNT(o.order_id) > 2
ORDER BY liczba_zamowien DESC
LIMIT 10;
```

---

## 🧩 Zadanie 2: Produkty z przychodem powyżej 3000 zł

### 🎯 Cel:
Wyświetl `product_id`, `name` oraz łączny przychód ze sprzedaży (`SUM(quantity * price)`) dla produktów, które przyniosły więcej niż 3000 zł.

### ✅ Zapytanie:

```sql
SELECT p.product_id, p.name, SUM(oi.quantity * p.price) AS przychod
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.product_id
HAVING SUM(oi.quantity * p.price) > 3000;
```

---

## 🧩 Zadanie 3: Ostatnie 5 zamówień z danymi klienta

### 🎯 Cel:
Wyświetl `order_id`, `order_date`, `first_name`, `last_name`, `status` dla 5 najnowszych zamówień.

### ✅ Zapytanie:

```sql
SELECT o.order_id, o.order_date, c.first_name, c.last_name, o.status
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
ORDER BY o.order_date DESC
LIMIT 5;
```

---

