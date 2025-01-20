Bufory to nic innego jak **tablice w pamięci**, które przechowują dane tymczasowo, aby umożliwić bardziej efektywne operacje odczytu i zapisu.

**Czym są bufory technicznie?**
Bufory to zwykle tablice w pamięci (np. `byte[]` lub `char[]`), które służą do przechowywania:
- Porcji danych odczytanych z jakiegoś źródła (np. pliku, gniazda sieciowego).
- Porcji danych do zapisania w jakieś miejsce (np. plik, konsola, gniazdo sieciowe).
Bufory są tworzone w celu zmniejszenia liczby operacji wejścia/wyjścia (IO), które są kosztowne pod względem wydajności.


| Bez bufora                                                                                                                                                                                                     | Z buforem                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Każda operacja odczytu powoduje, że program żąda danych od systemu operacyjnego. System operacyjny musi uzyskać dostęp do dysku, co jest wolne. Dla pliku o rozmiarze 1MB wykonasz 1 048 576 operacji odczytu. | Bufor działa jak pośrednik. Zamiast odczytywać dane bajt po bajcie, program odczytuje cały blok danych naraz (np. 8192 bajty) i zapisuje je do bufora. Dla tego samego pliku o rozmiarze 1 MB i buforze 8192 bajtów potrzebujesz tylko 128 operacji odczytu. |
**Jak wygląda bufor od strony pamięci?**
Bufory w Javie są zaimplementowane jako tablice:
- **Buffered Streams w IO**: Wewnętrznie używają tablic bajtów lub znaków.
- **Bufory w NIO**: Są to bardziej zaawansowane struktury oparte na tablicach, które przechowują dane i umożliwiają dodatkowe operacje, takie jak przesunięcia wskaźnika w buforze.

***Bufory w NIO - zaawansowane funkcje***
Bufory w NIO `java.nio.Buffer` są bardziej zaawansowane niż zwykłe tablice. Oferują dodatkowe funkcjonalności:
1. **Wskaźniki pozycji i limitu:
	- `position` - gdzie aktualnie jesteśmy w buforze.
	- `limit` - gdzie kończą się dostępne dane w buforze.
	- `capacity` - maksymalny rozmiar bufora.
2. **Operacje odczytu i zapisu**:
	- `put()` - dodawanie danych do bufora.
	- `get()` - pobieranie danych z bufora.
3. **Bufory mogą być "direct"**
	- Dane są przechowywane bezpośrednio w pamięci poza stertą (heap), co przyśpiesza ich przetwarzanie.
