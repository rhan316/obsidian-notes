Indeksy w SQL to struktury danych, które przyśpieszają wyszukiwanie informacji w tabeli - działają jak spis treści w książce.
Zamiast przeszukiwać całą tabelę, indeks pozwala na szybkie odnalezienie wierszy spełniających warunek zapytania.

### Rodzaje indeksów w SQL

**Indeks podstawowy (Primary Index)**
*Jak numery stron w książce - każda strona ma unikalny numer*
- Tworzony automatycznie dla klucza głównego `PRIMARY KEY`
- Gwarantuje unikalność wartości i szybkie wyszukiwanie
- Zazwyczaj jest indeksem klastrowym
```sql
CREATE TABLE users (
	id INT PRIMARY KEY, -- Indeks tworzony automatycznie
	name VARCHAR(100)
);
```

**Indeks unikalny (Unique Index)**
*Jak numer telefonu - każda osoba ma unikalny numer*
Zapewnia unikalność wartości w danej kolumnie.
Jest podobny do indeksu `PRIMARY KEY`, ale może istnieć wiele unikalnych indeksów w jednej tabeli.
```sql
CREATE UNIQUE INDEX idx_email ON users(email);
```

**Indeks klastrowany (Clustered Index)**
*Jak uporządkowanie książki na półce - fizyczne ułożenie danych w tabeli zależy od indeksów*
- Każda tabela może mieć tylko jeden indeks klastrowany.
- Wpływa na fizyczne rozmieszczenie danych na dysku.
- Wyszukiwanie po indeksie klastrowanym jest bardzo szybkie.
- W MySQL indeks klastrowany jest automatycznie tworzony w kluczu głównym `PRIMARY KEY`
```sql
CREATE CLUSTERED INDEX idx_orders ON orders(order_date);
```

**Indeks nieklastrowany (Non-clustered Index)**
*Jak index na końcu książki - dane są w innej kolejności niż w spisie*
Może istnieć wiele indeksów nieklastrowanych na jednej tabeli.
Przechowuje odniesienia (wskaźniki) do rzeczywistych wierszy w tabeli, zamiast zmieniać ich fizyczne rozmieszczenie.
```sql
CREATE INDEX idx_name ON users(name);
```

**Indeks wielokolumnowy (Composite Index)**
*Jak katalog w bibliotece - książki są sortowane najpierw według tematu, potem autora*
Tworzony na wielu kolumnach jednocześnie.
```sql
CREATE INDEX idx_full_name ON users(last_name, first_name);
```
Optymalizuje zapytania, które filtrują po obu kolumnach `WHERE last_name = 'kowalski' AND first_name = 'Jan'`;

**Indeks pełnotekstowy (Full_Text Index)**
*Jak Google - pozwala na szybkie wyszukiwanie w długich tekstach*
Służy do wyszukiwania fraz w dużych tekstach `TEXT, VARCHAR`
Umożliwia szybkie `MATCH()` zamiast wolnych `LIKE %fraza%`
```sql
CREATE FULLTEXT INDEX idx_text ON articles(content);

SELECT * FROM articles WHERE MATCH(content) AGAINST('sztuczna inteligencja');
```

**Indeks bitmapowy (Bitmap Index)**
*Jak lista obecności - szybkie filtrowanie wartości o małej liczbie unikalnych wartości*
Optymalny dla kolumn o niskiej kardynalności (np. płeć, status zamówienia)