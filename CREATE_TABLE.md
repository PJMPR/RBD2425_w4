# 🛍️ E-commerce Database Schema (MariaDB)

Dokumentacja struktury bazy danych dla sklepu internetowego.  

## 👤 Table: `customers`

Dane klientów sklepu: imię, nazwisko, e-mail, numer telefonu, data rejestracji.

```sql
CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20),
    registration_date DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

## 📍 Table: `addresses`

Adresy klientów – tabela powiązana z `customers`.

```sql
CREATE TABLE addresses (
    address_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    street VARCHAR(100),
    city VARCHAR(50),
    zip_code VARCHAR(10),
    country VARCHAR(50),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

---

## 🛒 Table: `products`

Katalog produktów – zawiera nazwę, opis, cenę i informację, czy produkt jest aktywny. Zawiera warunek `CHECK` na cenę.

```sql
CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL CHECK (price >= 0),
    active BOOLEAN DEFAULT TRUE
);
```

---

## 🏬 Table: `inventory`

Stany magazynowe produktów – tabela z aktualizującą się datą i ograniczeniem ilości do wartości >= 0.

```sql
CREATE TABLE inventory (
    product_id INT PRIMARY KEY,
    quantity INT DEFAULT 0 CHECK (quantity >= 0),
    last_updated DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

---

## 🧾 Table: `orders`

Zamówienia złożone przez klientów – zawiera status zamówienia z ograniczonymi wartościami przez `CHECK`.

```sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50) DEFAULT 'new' CHECK (status IN ('new', 'shipped', 'delivered', 'cancelled')),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

---

## 📦 Table: `order_items`

Pozycje w zamówieniach – relacja wiele-do-wielu pomiędzy zamówieniami i produktami. Ilość musi być większa od zera.

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL CHECK (quantity > 0),
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

---

## ✅ Summary of CHECK Constraints

W bazie używamy następujących ograniczeń `CHECK`:
- `price >= 0` w `products`
- `quantity >= 0` w `inventory`
- `quantity > 0` w `order_items`
- `status IN (...)` w `orders`

Dzięki temu zabezpieczamy dane na poziomie bazy.

---
