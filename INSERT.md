
# Komenda `INSERT` w MariaDB – Przykłady z użyciem tabel

## 🔹 1. Podstawowa składnia `INSERT INTO`

```sql
INSERT INTO nazwa_tabeli (kolumna1, kolumna2, ...) VALUES (wartość1, wartość2, ...);
```

---

## 🔸 PRZYKŁADY DLA TABEL

### ✅ Wstawienie nowego klienta do tabeli `customers`

```sql
INSERT INTO customers (first_name, last_name, email)
VALUES ('Anna', 'Nowak', 'anna.nowak@example.com');
```

- Nie podajemy `customer_id`, bo to `AUTO_INCREMENT`.
- Nie podajemy `registration_date`, bo ma domyślną wartość `CURRENT_TIMESTAMP`.

---

### ✅ Wstawienie adresu klienta do tabeli `addresses`

Zakładamy, że klient o `customer_id = 1` już istnieje:

```sql
INSERT INTO addresses (customer_id, street, city, zip_code, country)
VALUES (1, 'ul. Kwiatowa 12', 'Warszawa', '00-001', 'Polska');
```

---

### ✅ Dodanie produktu do `products`

```sql
INSERT INTO products (name, description, price)
VALUES ('Laptop', 'Nowoczesny laptop z 16GB RAM', 3499.99);
```

---

### ✅ Dodanie stanu magazynowego do `inventory`

Załóżmy, że `product_id = 1`:

```sql
INSERT INTO inventory (product_id, quantity)
VALUES (1, 10);
```

---

### ✅ Złożenie zamówienia w `orders`

```sql
INSERT INTO orders (customer_id, status)
VALUES (1, 'new');
```

---

### ✅ Dodanie pozycji zamówienia do `order_items`

Załóżmy, że `order_id = 1`, `product_id = 1`:

```sql
INSERT INTO order_items (order_id, product_id, quantity)
VALUES (1, 1, 2);
```

---

## 🔹 2. INSERT bez podania kolumn

```sql
INSERT INTO products
VALUES (NULL, 'Smartfon', 'Nowy model', 1999.00, TRUE);
```

---

## 🔹 3. INSERT z wieloma wierszami

```sql
INSERT INTO products (name, description, price)
VALUES 
  ('Tablet', '10-calowy ekran', 899.00),
  ('Monitor', '27 cali 4K', 1299.00);
```

---

## 🔹 4. INSERT ... SELECT

```sql
INSERT INTO temp_customers (first_name, last_name, email)
SELECT first_name, last_name, email
FROM customers
WHERE email LIKE '%@example.com';
```

---

## 🔹 5. INSERT IGNORE / ON DUPLICATE KEY UPDATE

### ✅ `INSERT IGNORE`

```sql
INSERT IGNORE INTO customers (first_name, last_name, email)
VALUES ('Anna', 'Nowak', 'anna.nowak@example.com');
```

### ✅ `ON DUPLICATE KEY UPDATE`

```sql
INSERT INTO customers (first_name, last_name, email)
VALUES ('Anna', 'Nowak', 'anna.nowak@example.com')
ON DUPLICATE KEY UPDATE first_name = VALUES(first_name), last_name = VALUES(last_name);
```
