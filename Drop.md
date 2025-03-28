
# 💥 DROP TABLE – MariaDB

Komenda `DROP TABLE` służy do **usuwania całych tabel** z bazy danych – razem z ich strukturą i wszystkimi danymi.

---

## 🧨 Podstawowa składnia

```sql
DROP TABLE table_name;
```

Usuwa tabelę o nazwie `table_name`.

---

## ✅ Bezpieczna wersja

```sql
DROP TABLE IF EXISTS table_name;
```

Nie wygeneruje błędu, jeśli tabela nie istnieje.

---

## 🧾 Przykłady (e-commerce database)

### Usuń tabelę `orders`:
```sql
DROP TABLE orders;
```

### Usuń tabelę `customers` tylko jeśli istnieje:
```sql
DROP TABLE IF EXISTS customers;
```

---

## ⚠️ Uwaga – operacja nieodwracalna

`DROP TABLE`:
- Usuwa wszystkie dane
- Usuwa strukturę tabeli (kolumny, typy)
- Usuwa klucze (`PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, itd.)
- Usuwa indeksy i relacje

---

## 🔗 Klucze obce – problem z zależnościami

Jeśli inne tabele mają klucz obcy do tej tabeli (np. `order_items → orders`), pojawi się błąd:

```
Cannot delete or update a parent row: a foreign key constraint fails
```

### Możliwe rozwiązania:
1. Usuń najpierw tabele zależne:
```sql
DROP TABLE order_items;
DROP TABLE orders;
```

2. Tymczasowo wyłącz sprawdzanie kluczy obcych:
```sql
SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE orders;
SET FOREIGN_KEY_CHECKS = 1;
```

---

## 🔁 DROP vs DELETE vs TRUNCATE

| Komenda           | Co robi                                      | Usuwa strukturę tabeli? |
|-------------------|-----------------------------------------------|--------------------------|
| `DROP TABLE`      | Usuwa całą tabelę i dane                      | ✅ Tak                  |
| `TRUNCATE TABLE`  | Czyści dane, zachowuje strukturę              | ❌ Nie                 |
| `DELETE FROM ...` | Usuwa dane (można z WHERE)                    | ❌ Nie                 |

---

## 📂 Podsumowanie

`DROP TABLE` to silna komenda – bardzo użyteczna, ale też niebezpieczna.  
Zawsze warto robić backup przed jej użyciem lub stosować `IF EXISTS`.

---
