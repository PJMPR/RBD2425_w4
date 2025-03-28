
# Komenda `UPDATE` w MariaDB – Wyjaśnienie i przykłady

Komenda `UPDATE` służy do modyfikowania danych w istniejących wierszach tabeli.

---

## 🔹 Podstawowa składnia

```sql
UPDATE nazwa_tabeli
SET kolumna1 = nowa_wartosc1,
    kolumna2 = nowa_wartosc2
WHERE warunek;
```

---

## 🔸 Uwaga

🛑 **Bez klauzuli `WHERE` zostaną zaktualizowane wszystkie rekordy!**

---

## 🔸 Przykłady na Twoich tabelach

### ✅ 1. Aktualizacja adresu klienta

```sql
UPDATE addresses
SET street = 'ul. Nowa 15', city = 'Kraków'
WHERE customer_id = 1;
```

---

### ✅ 2. Zmiana statusu zamówienia

```sql
UPDATE orders
SET status = 'shipped'
WHERE order_id = 1;
```

---

### ✅ 3. Dezaktywacja produktu

```sql
UPDATE products
SET active = FALSE
WHERE product_id = 2;
```

---

### ✅ 4. Obniżenie ceny wszystkich produktów o 10%

```sql
UPDATE products
SET price = price * 0.9;
```

---

### ✅ 5. Zmniejszenie stanu magazynowego

```sql
UPDATE inventory
SET quantity = quantity - 3
WHERE product_id = 1;
```

---

## 🔹 `UPDATE` z `JOIN`

```sql
UPDATE inventory i
JOIN products p ON i.product_id = p.product_id
SET i.quantity = 0
WHERE p.active = FALSE;
```

---

## 🔹 `UPDATE` z `LIMIT`

```sql
UPDATE products
SET price = price + 100
ORDER BY price ASC
LIMIT 3;
```

---

## 🔹 `UPDATE` z podzapytaniem (`subquery`)

### ✅ Generowanie adresów e-mail, jeśli brak

```sql
UPDATE customers
SET email = CONCAT(first_name, '.', last_name, '@example.com')
WHERE email IS NULL;
```

---

### ✅ Anulowanie zamówień, w których ilość produktu wynosi 0

```sql
UPDATE orders
SET status = 'cancelled'
WHERE order_id IN (
    SELECT order_id FROM order_items WHERE quantity = 0
);
```

---
