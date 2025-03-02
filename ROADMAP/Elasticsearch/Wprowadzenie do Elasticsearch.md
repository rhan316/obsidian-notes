*Elasticsearch* to wyszukiwarka pełnotekstowa i baza danych NoSQL, zoptymalizowana pod kątem szybkiego wyszukiwania dużych zbiorów danych.
Działa na zasadzie *indeksowania dokumentów JSON* i umożliwia wyszukiwanie w ułamku sekundy.
Jest często używany w Spring Boot do zaawansowanego filtrowania, analizy logów i autouzupełnienia wyszukiwan.

*Analogia: Elasticsearch to Google dla Twojej aplikacji - możesz wyszukiwać dane niemal natychmiast, nawet w milionach rekordów!*

### Jak Elasticsearch działa w Spring Boot?
Spring Boot integruje się z Elasticsearch za pomocą Spring Data Elasticsearch, co umożliwia:
- Indeksowanie danych (zamiast klasycznych tabel SQL)
- Wyszukiwanie pełnotekstowe (`match`, `wilcard`, `fuzzy search`)
- Filtrowanie i agregacje (np. znajdowanie najpopularniejszych produktów)
- Obsługę zapytań REST API (dzięki Elasticsearch jako serwerowi HTTP)

### Jak Elasticsearch przechowuje dane?
W SQL dane przechowywane są w tabelach, wierszach i kolumnach.
W Elasticsearch dane przechowywane są w indeksach, dokumentach i shardach.

| SQL         | Elasticsearch (NoSQL) |
| ----------- | --------------------- |
| Baza danych | Klaster `Cluster`     |
| Tabela      | Indeks `Index`        |
| Wiersz      | Dokument `Document`   |
| Kolumna     | Pole `Field`          |
Przykład dokumentu JSON w Elasticsearch (odpowiednik wiersza SQL)
```json
{
	"id": 1,
	"name": "Laptop",
	"category": "Electronics",
	"price": 45000.00
}
```
Dane są niezależnymi dokumentami JSON - Elasticsearch nie używa relacji między tabelami!!!!

### Jak działa wyszukiwanie w Elasticsearch?

Indeksowanie zamiast klasycznego SQL `SELECT`
Gdy dokumenty są dodawane, Elasticsearch tworzy indeksy na podstawie analizy treści.
Podczas wyszukiwania nie przeszukuje całej bazy, lecz korzysta z wcześniej utworzonych indeksów.

Przykład zapytania w Elasticsearch (odpowiednik `SELET * FROM products WHERE name = 'Laptop'` w SQL)
```json
GET products/_search
{
	"query": {
		"match": { "name": "Laptop" }
	}
}
```
Elasticsearch szybko odnajduje pasujące dokumenty, zamiast skanować wszystkie dane.

### Jak działa indeksowanie w Elasticsearch?
Elasticsearch używa odwrotnego indeksu (Inverted Index) - podobnie jak indeks na końcu książki.

*Jak działa odwrotny indeks?*
ES rozkłada tekst na **tokeny (słowa kluczowe)**.
Tworzy mapę: słowo -> lista dokumentów, w których występuje.
Wyszukiwanie jest błyskawiczne, bo zamiast przeszukiwać całą bazę, Elasticsearch sprawdza tylko indeks!

| Słowo  | Dokumenty |
| ------ | --------- |
| Laptop | 1, 5, 9   |
| Gaming | 2, 5, 7   |
Elasticsearch natychmiast odnajduje pasujące dokumenty!

### Jak Elasticsearch skaluje się w dużych zbiorach danych?
Podział danych na **shardy (Shard Splitting)** - ES dzieli indeksy na mniejsze części (shardy), które mogę być przechowywane na różnych serwerach.
Replikacja danych - każdy shard może mieć kopie zapasowe (replica shards), co zwiększa odporność na awarie.

*Jak to działa w praktyce?*
- Indeks podzielony na shardy (np. 3 shardy dla indeksu `products`)
- Każdy shard przechowywany na innym serwerze
- Jeśli jeden serwer padnie, ES korzysta z kopii (replica shards)

**Zalety ES jako NoSQL**
1. Szybkość - odwrotny indeks pozwala na błyskawiczne wyszukiwanie
2. Elastyczność - przechowuje dokumenty JSON, bez sztywnej struktury tabel
3. Skalowalność - dzielenie indeksów na shardy pozwala na obsługę dużych zbiorów danych
4. Obsługa wyszukiwania pełnotekstowego - np. `match, wilcard, fuzzy search`
5. Analiza i agregacje - ES pozwala na zaawansowane filtrowanie i statystyki