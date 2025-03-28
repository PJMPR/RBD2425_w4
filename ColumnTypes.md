
# 🗂️ MariaDB Column Types – Przegląd

Przegląd najczęściej używanych typów danych w bazie danych **MariaDB**. 

---

## 🔢 Typy liczbowe (Number types)

| Typ            | Opis                                              | Przykład                    |
|----------------|---------------------------------------------------|-----------------------------|
| `TINYINT`      | Mała liczba całkowita (-128 do 127)               | `age TINYINT`               |
| `SMALLINT`     | Liczba całkowita (2 bajty)                        | `stock SMALLINT`            |
| `MEDIUMINT`    | Średnia liczba całkowita                          | `views MEDIUMINT`           |
| `INT` / `INTEGER` | Liczba całkowita (standardowo używana)        | `id INT AUTO_INCREMENT`     |
| `BIGINT`       | Duża liczba całkowita (np. do finansów)           | `balance BIGINT`            |
| `DECIMAL(m,d)` | Liczba dziesiętna z precyzją (np. ceny)           | `price DECIMAL(10,2)`       |
| `FLOAT(p)`     | Liczba zmiennoprzecinkowa                         | `rating FLOAT`              |
| `DOUBLE`       | Dokładniejsza liczba zmiennoprzecinkowa           | `temperature DOUBLE`        |

---

## 📝 Typy tekstowe (String types)

| Typ             | Opis                                           | Przykład                      |
|------------------|------------------------------------------------|-------------------------------|
| `CHAR(n)`        | Stała długość tekstu                          | `code CHAR(3)`                |
| `VARCHAR(n)`     | Zmienna długość (najczęściej używane)         | `name VARCHAR(100)`           |
| `TEXT`           | Dłuższy tekst (do 65 KB)                      | `description TEXT`            |
| `TINYTEXT`       | Krótki tekst (do 255 bajtów)                  | `short_note TINYTEXT`         |
| `MEDIUMTEXT`     | Tekst do 16 MB                                | `article MEDIUMTEXT`          |
| `LONGTEXT`       | Tekst do 4 GB                                 | `terms LONGTEXT`              |
| `ENUM(...)`      | Lista dozwolonych wartości                    | `status ENUM('new','paid')`   |
| `SET(...)`       | Zbiór możliwych wartości (wielokrotny wybór) | `tags SET('sale','hot')`      |

---

## ⏰ Typy daty i czasu (Date and Time types)

| Typ         | Opis                                        | Przykład                        |
|--------------|---------------------------------------------|---------------------------------|
| `DATE`       | Data (YYYY-MM-DD)                          | `birthdate DATE`                |
| `DATETIME`   | Data i czas                                | `created_at DATETIME`           |
| `TIMESTAMP`  | Data i czas z automatyczną aktualizacją    | `updated_at TIMESTAMP`          |
| `TIME`       | Godzina (HH:MM:SS)                         | `duration TIME`                 |
| `YEAR`       | Rok (YYYY)                                 | `release_year YEAR`             |

---

## 🔘 Typy logiczne i binarne (Boolean / Binary)

| Typ        | Opis                               | Przykład                 |
|------------|------------------------------------|--------------------------|
| `BOOLEAN`  | Wartość logiczna (`TINYINT(1)`)    | `active BOOLEAN`         |
| `BIT(n)`   | Dane binarne (np. flagi)           | `flags BIT(8)`           |
| `BINARY(n)` / `VARBINARY(n)` | Ciągi bajtów     | `token VARBINARY(255)`   |
| `BLOB`     | Dane binarne (np. pliki, obrazy)   | `photo BLOB`             |

---

## ⚙️ Dodatkowe opcje kolumn

| Opcja               | Opis |
|---------------------|------|
| `NOT NULL`          | Pole obowiązkowe |
| `DEFAULT`           | Domyślna wartość |
| `AUTO_INCREMENT`    | Automatyczne zwiększanie wartości |
| `UNIQUE`            | Wartość unikalna |
| `PRIMARY KEY`       | Klucz główny tabeli |
| `FOREIGN KEY`       | Klucz obcy (relacja z inną tabelą) |
| `CHECK (warunek)`   | Ograniczenie logiczne, np. `CHECK (price >= 0)` |

---

## 📌 Uwagi

- Do wartości pieniężnych używaj `DECIMAL`, nie `FLOAT`.
- Do statusów zamówień używaj `ENUM` lub `VARCHAR` z `CHECK`.
- `VARCHAR` jest najczęściej używanym typem dla nazw i opisów.

---

