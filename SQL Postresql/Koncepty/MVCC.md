**MVCC (Multiversion Concurrency Control)** to mechanizm kontroli współbieżności w PostgreSQL, która pozwala wielu transakcjom na jednoczesny dostęp do bazy danych bez blokowania odczytów i zapisów. Dzięki MVCC każda transakcja widzi **spójny stan bazy**, nawet jeśli inne transakcje równocześnie modyfikują dane.

### Jak działa MVCC?
PostgreSQL stosuje strategię **wersjonowania wierszy** - zamiast nadpisywać istniejące dane, tworzy nowe wersje wierszy. Stare wersje pozostają widoczne dla transakcji, które je utworzyły, a nowe są widoczne dla nowych transakcji.
```pgsql
 id | name 
----+------
  1 | Alice
```
Transakcja A rozpoczyna pracę i czyta użytkownika "Alice".
Transakcja B aktualizuje "Alice" na "Alicia".
Transakcja B jeszcze nie zatwierdziła zmian (COMMIT).
Transakcja A nadal widzi starą wersję ("Alice"), ponieważ działa na migawce (snapshot) z chwili jej rozpoczęcia.
Transakcja B zatwierdza zmiany.
Nowe transakcje widzą już "Alicia", ale stara wersja jest nadal w bazie do momentu, aż PGSQL ją usunie (VACUUM).

### Kluczowe koncepcje MVCC:

**XMIN i XMAX - identyfikatory wersji**
Każdy wiersz w PostgreSQL ma ukryte pola:
- xmin - numer transakcji, która go utworzyła.
- xmax - numer transakcji, która go usunęła (jeśli wiersz został skasowany lub zaktualizowany).
```sql
SELECT ctid, xmin, xmax, * FROM users;
```

**SNAPSHOT - Migawka danych**
Każda transakcja widzi stan bazy danych z momentu jej rozpoczęcia. Jeśli inna transakcja modyfikuje dane, nowa wersja wiersza jest tworzona, ale nie jest widoczna dla trwających transakcji.

**VACUUM - Oczyszczanie starych wersji**
Stare wersje wierszy zajmują miejsce, więc PostgreSQL regularnie uruchamia **autovacuum**, aby je usuwać.

