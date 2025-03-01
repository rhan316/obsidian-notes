W kontekście SQL "Failure Modes" (tryb awarii) odnoszą się do różnych sposobów, w jakie operacje SQL mogą się nie powieść. Może to obejmować błędy związane z integracją danych, blokadami, ograniczeniami wydajności, błędami syntaktycznymi itp.

Pomyśl o systemie baz danych jak o kuchni restauracyjnej: kucharze (serwer SQL) obsługują zamówienia (zapytania SQL), a różne rzeczy mogą pójść nie tak - od braku składników (bark danych), przez spalone dania (błędy logiczne), po blokowanie się kucharzy nawzajem (problemy z blokadami).

### Najczęstsze tryby awarii w SQL:

**Syntax Errors (Błędy składniowe)**
Powstają, gdy składnia SQL jest niepoprawna, np. zapomniane słowo kluczowe lub źle sformułowane zapytanie
```sql
SELEC * FROM users; -- Błąd: powinno być SELECT!
```
*Rozwiązanie: Poprawna składnia i testowanie zapytań przed wykonaniem*

**Constraint Violations (Naruszenie ograniczeń)**
Dotyczy naruszenia ograniczeń takich jak `PRIMARY`, `UNIQUE`, `FOREIGN KEY`, `NOT NULL`, `CHECK`.
```sql
INSERT INTO users (id, email) VALUES (1, 'test@example.com');
INSERT INTO users (id, email) VALUES (1, 'test@example.com');
-- Błąd: PRIMARY KEY id=1 już istnieje!
```
*Rozwiązanie: Upewnić się, że zestawiane dane spełniają ograniczenia*

**Deadlocks (Zakleszczenie)**
Występuje, gdy dwa zapytania blokują się nawzajem, czekając na zasoby.
Przykład:
1. Transakcja A blokuje wiersz 1 i chce dostać wiersz 2
2. Transakcja B blokuje wiersz 2 i chce dostać wiersz 1
3. Obie transakcje czekają w nieskończoność.
*Rozwiązanie: Optymalizacja kolejności wykonywania zapytań i timeouty.*

**Locking Issues (Problemy z blokadami)**
Jeśli transakcja blokuje wiersze zbyt długo, inne zapytania mogą czekać.
Może to prowadzić do niskiej wydajności lub blokady systemu.
*Rozwiązanie: Używanie odpowiednich poziomów izolacji: `RED COMMITTED`, `SERIALIZABLE` itp.*

**Transaction Failures (Błędy transakcji)**
Jeśli transakcja się nie zatwierdzi `COMMIT`, wszystkie zmiany są cofane `ROLLBACK`.
```sql
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
ROLLBACK; -- Wszystkie zmiany cofnięte
```
*Rozwiązanie: Upewnić się, że transakcja kończy się poprawnym `COMMIT`*

**Performance Issues (Problemy wydajnościowe)**
Nieoptymalne zapytania mogę zużywać zbyt dużo zasobów.
```sql
SELECT * FROM large_table WHERE LOWER(name) = 'john';
-- Problem: Funkcja LOWER() uniemożliwia użycie indeksu
```
*Rozwiązanie: Indeksy, popraw struktury zapytań, analiza planu wykonania `EXPLAIN ANALYZE`*