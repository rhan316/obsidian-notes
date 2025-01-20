Kanały `Channels` w Java NIO to nowoczesne podejście do obsługi wejścia/wyjścia, które jest bardziej elastyczne i wydajne niż tradycyjne strumienie `InputStream/OutputStream` w pakiecie `java.io`. Kanały umożliwiają odczyt i zapis danych bezpośrednio do/ z buforów `Buffers` i wspierają operacje nieblokujące oraz równoległe.

---
***Podstawowe cechy kanałów***

**Obsługa buforów (Buffers)**
	Kanały nie operują bezpośrednio na danych, lecz współpracują z buforami, które przechowują dane tymczasowo.
	Dzięki temu można wydajnie przetwarzać dane w segmentach, zamiast odczytywać je znak po znaku.

**Dwukierunkowość**
	Kanały mogą działać zarówno jako wejście, jak i wyjście (np. `FileChannel`), co odróżnia je od tradycyjnych strumieni.

**Nieblokujące I/O**
	Obsługują operacje nieblokujące, co oznacza, że wątek nie musi czekać na zakończenie operacji wejścia/wyjścia (np. `SocketChannel`).

**Integracja z Selectorami**
	Kanały można monitorować za pomocą obiektu `Selector`, co pozwala jednemu wątkowi obsługiwać wiele kanałów jednocześnie.

**Wysoka wydajność**
	Kanały korzystają z funkcji systemu operacyjnego, takich jak *Directory Memory Access (DMA)*, co pozwala na szybkie przesyłanie danych między urządzeniami bez pośrednictwa aplikacji.

---
***Typy kanałów w NIO***

1. **FileChannel** - Służy do operacji na plikach. Pozwala na odczyt/zapis/poruszanie się po pliku w sposób losowy (random access).
2. **SocketChannel** - Umożliwia komunikację sieciową za pomocą gniazd (sockets). Obsługuje połączenia TCP.
3. **ServerSocketChannel** - Obsługuje serwery TCP (nasłuchiwanie na połączenia).
4. **DatagramChannel** - Umożliwia komunikację opartą na protokole UDP.
5. **Pipe** - Reprezentuje kanał jednostronnej komunikacji między dwoma wątkami w tej samej aplikacji.

---
**Obsługa plików (FileChannel)** Wydajny odczyt/zapis dużych plików dzięki metodom takim jak `transferTo()` i `transferFrom()`, które wykorzystują optymalizacje systemowe. Losowy dostęp do danych w pliku, np. edycja tylko określonego fragmentu.

