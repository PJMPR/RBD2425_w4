
# 🔗 FOREIGN KEY – Tworzenie, usuwanie i dobre praktyki (MariaDB)

Relacje (`FOREIGN KEY`) w MariaDB pozwalają na tworzenie powiązań między tabelami – kluczowych dla integralności danych w relacyjnych bazach danych.

---

## 📌 Co to jest relacja (klucz obcy)?

Relacja (`FOREIGN KEY`) łączy dane z dwóch tabel – np. `orders.customer_id` wskazuje na `customers.customer_id`.

---

## ✅ Tworzenie relacji

### 🏗 1. W `CREATE TABLE`

```sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    order_date DATETIME,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

---

### 🛠 2. Później przez `ALTER TABLE`

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
FOREIGN KEY (customer_id) REFERENCES customers(customer_id);
```

---

## ❌ Usuwanie relacji

### Krok 1 – sprawdź nazwę ograniczenia:
```sql
SHOW CREATE TABLE orders;
```

### Krok 2 – usuń klucz:
```sql
ALTER TABLE orders
DROP FOREIGN KEY fk_orders_customer;
```

---

## 🔐 Dodatkowe opcje przy relacjach

```sql
FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
ON DELETE CASCADE
ON UPDATE CASCADE;
```

| Opcja                | Działanie                                                                 |
|----------------------|--------------------------------------------------------------------------|
| `ON DELETE CASCADE`  | Usunięcie klienta powoduje usunięcie jego zamówień                      |
| `ON DELETE SET NULL` | Po usunięciu klienta, `customer_id` w `orders` ustawiany jest na NULL   |
| `ON DELETE RESTRICT` | Nie pozwala usunąć klienta, jeśli ma zamówienia (domyślnie)             |

---

## ❓ Tworzyć relacje od razu czy później?

| Podejście                      | Zalety                                     | Wady                             |
|-------------------------------|--------------------------------------------|----------------------------------|
| 🔹 W `CREATE TABLE`           | Przejrzystość, spójność od początku        | Musisz znać zależności wcześniej |
| 🔹 Przez `ALTER TABLE`        | Elastyczność, dobre przy migracjach        | Można zapomnieć lub źle dodać    |

✅ Rekomendacja:
- Twórz relacje w `CREATE TABLE`, jeśli projektujesz bazę od zera
- Użyj `ALTER TABLE`, gdy integrujesz nowe dane lub robisz migrację

---

## 🧾 Praktyczne przykłady

### Połączenie `orders` z `customers`:

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
FOREIGN KEY (customer_id) REFERENCES customers(customer_id);
```

### Połączenie `order_items` z `orders` i `products`:

```sql
ALTER TABLE order_items
ADD CONSTRAINT fk_items_order
FOREIGN KEY (order_id) REFERENCES orders(order_id);

ALTER TABLE order_items
ADD CONSTRAINT fk_items_product
FOREIGN KEY (product_id) REFERENCES products(product_id);
```

---

## 📂 Podsumowanie

- Relacje (`FOREIGN KEY`) zabezpieczają spójność danych
- Można je dodać w `CREATE TABLE` lub później (`ALTER TABLE`)
- Dobrze nazywaj ograniczenia (`fk_nazwa_tabeli_klucz`)
- Korzystaj z `ON DELETE` / `ON UPDATE`, by dopasować się do logiki aplikacji

---
