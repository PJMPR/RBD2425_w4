
# ✂️ TRUNCATE TABLE – MariaDB

Komenda `TRUNCATE TABLE` służy do **szybkiego usuwania wszystkich danych z tabeli**, bez zmiany jej struktury.

---

## 🧨 Składnia

```sql
TRUNCATE TABLE table_name;
```

Usuwa wszystkie rekordy z tabeli `table_name`.

---

## 🧾 Przykład (e-commerce)

Wyczyść dane zamówień:

```sql
TRUNCATE TABLE orders;
```

---

## 🔍 Różnice: `TRUNCATE` vs `DELETE`

| Cecha                  | `DELETE FROM`              | `TRUNCATE TABLE`                  |
|------------------------|----------------------------|-----------------------------------|
| Usuwa dane             | ✅ Tak                     | ✅ Tak                            |
| Usuwa strukturę tabeli | ❌ Nie                     | ❌ Nie                            |
| `WHERE` możliwe?       | ✅ Tak                     | ❌ Nie                            |
| Cofnięcie (`ROLLBACK`) | ✅ Czasem                  | ❌ Zwykle nie                     |
| Reset AUTO_INCREMENT   | ❌ Zwykle nie              | ✅ Tak                            |
| Szybkość               | 🐢 Wolniejszy              | ⚡ Szybszy                        |

---

## ✅ Kiedy używać?

- Gdy chcesz **wyczyścić całą tabelę**
- Do **resetu danych testowych**
- Gdy nie potrzebujesz szczegółowej kontroli (`WHERE`)
- Dla **wydajności**

---

## ⚠️ Uwaga

- Operacja nieodwracalna
- Nie działa z `WHERE`
- Może nie zadziałać przy `FOREIGN KEY`

---

## 🔗 Klucze obce

MariaDB może zablokować `TRUNCATE`, jeśli inne tabele odwołują się do tej przez `FOREIGN KEY`.

Możesz tymczasowo wyłączyć sprawdzanie kluczy:

```sql
SET FOREIGN_KEY_CHECKS = 0;
TRUNCATE TABLE orders;
SET FOREIGN_KEY_CHECKS = 1;
```

---

## 🧪 Przykłady

Wyczyść klientów:

```sql
TRUNCATE TABLE customers;
```

Zresetuj produkty testowe:

```sql
TRUNCATE TABLE products;
```

---
