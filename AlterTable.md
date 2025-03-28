
# 🔧 ALTER TABLE – MariaDB Examples for E-commerce Database

Przykłady użycia komendy `ALTER TABLE` w bazie danych **MariaDB**, oparte na wcześniej zdefiniowanym schemacie sklepu internetowego.

---

## ✅ Add a new column

Dodanie nowej kolumny `newsletter_opt_in` do tabeli `customers`.

```sql
ALTER TABLE customers
ADD newsletter_opt_in BOOLEAN DEFAULT FALSE;
```

---

## 🧹 Drop a column

Usunięcie kolumny `phone` z tabeli `customers`.

```sql
ALTER TABLE customers
DROP COLUMN phone;
```

---

## ✏️ Rename a column

Zmiana nazwy kolumny `registration_date` na `created_at`.

```sql
ALTER TABLE customers
CHANGE COLUMN registration_date created_at DATETIME;
```

---

## 🔁 Modify column type

Zmiana typu kolumny `zip_code` z `VARCHAR(10)` na `VARCHAR(20)`.

```sql
ALTER TABLE addresses
MODIFY zip_code VARCHAR(20);
```

---

## 🧪 Add CHECK constraint

Dodanie warunku `CHECK` do kolumny `quantity` w `order_items`.

```sql
ALTER TABLE order_items
ADD CONSTRAINT chk_quantity CHECK (quantity > 0);
```

---

## 🔗 Add a FOREIGN KEY

Dodanie klucza obcego z `inventory.product_id` do `products.product_id`.

```sql
ALTER TABLE inventory
ADD CONSTRAINT fk_inventory_product
FOREIGN KEY (product_id) REFERENCES products(product_id);
```

Z opcją automatycznego usuwania:

```sql
... REFERENCES products(product_id)
ON DELETE CASCADE ON UPDATE CASCADE;
```

---

## 🧾 Change DEFAULT value

Zmienienie domyślnej wartości pola `status` w `orders`.

```sql
ALTER TABLE orders
ALTER COLUMN status SET DEFAULT 'pending';
```

Usunięcie domyślnej wartości:

```sql
ALTER TABLE orders
ALTER COLUMN status DROP DEFAULT;
```

---

## 🏷 Rename a table

Zmiana nazwy tabeli `orders` na `customer_orders`.

```sql
RENAME TABLE orders TO customer_orders;
```

---

## 📌 Podsumowanie możliwości `ALTER TABLE`

| Operacja                     | Przykład                                                   |
|------------------------------|------------------------------------------------------------|
| `ADD COLUMN`                 | Dodanie nowej kolumny do tabeli                           |
| `DROP COLUMN`                | Usunięcie kolumny z tabeli                                |
| `MODIFY`                     | Zmiana typu istniejącej kolumny                           |
| `CHANGE`                     | Zmiana nazwy kolumny i opcjonalnie jej typu              |
| `ADD CONSTRAINT`             | Dodanie ograniczenia (`CHECK`, `FOREIGN KEY`, `UNIQUE`)   |
| `DROP CONSTRAINT`            | Usunięcie ograniczenia                                     |
| `ALTER COLUMN ... DEFAULT`   | Ustawienie lub usunięcie wartości domyślnej              |
| `RENAME TO`                  | Zmiana nazwy tabeli                                       |

---

## 🧠 Wskazówki

- Uważaj przy `DROP COLUMN` – dane są tracone bezpowrotnie.
- `CHECK` constraints są wspierane od MariaDB 10.2+.
- Do zmian nazw kolumn zawsze podawaj typ danych (`CHANGE` wymaga typu!).
- Do dużych migracji warto użyć narzędzi typu `Liquibase`, `Flyway`, lub ORM.

---

