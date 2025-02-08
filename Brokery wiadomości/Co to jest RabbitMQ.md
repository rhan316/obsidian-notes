RabbitMQ to **broker wiadomości (ang. message broker)** - oprogramowanie pośredniczące, które umożliwia aplikacjom wymianę komunikatów w sposób asynchroniczny i zdecentralizowany. Jest to narzędzie do obsługi kolejek wiadomości, które działają zgodnie z modelem~={8} **publisher-subscribe i queue-base messaging**=~. RabbitMQ korzysta z protokołów~={8} AMQP (Advanced Message Queuing Protocol)=~ i może być używany w wielu językach, w tym w Javie.

Wyobraź sobie centrum logistyczne:
- ~={8}**Producent (producent wiadomości)**=~ - wysyła paczki (wiadomości) do centrum dystrybucji (RabbitMQ).
- Centrum przechowuje paczki w odpowiednich strefach (kolejkach).
- Kurierzy (odbiorcy) przychodzą po paczki i dostarczają je do adresatów.

RabbitMQ działa jak to centrum logistyczne:
- Zarządza wiadomościami, zapewniając ich dostarczenie.
- Organizuje komunikację między różnymi systemami, które mogą działać w różnych językach programowania i środowiskach.

---
RabbitMQ rozwiązuje problem ~={8}**asynchronicznej komunikacji**=~ między systemami. Oto główne zastosowania:

~={8}**Asynchroniczne przetwarzanie**=~: Umożliwia odciążenie głównych procesów aplikacji poprzez delegowanie czasochłonnych zadań do osobnych usług.

~={8}**Mikroserwisy**=~: RabbitMQ umożliwia komunikację między mikroserwisami w architekturze rozproszonej.

~={8}**Obsługa kolejek zadań**=~: Możesz dodawać zadania do kolejki i przetwarzać je w tle, np. generowanie raportów, przetwarzanie obrazów, wysyłanie e-maili.

~={8}**Model publish-subscribe**=~: Jedna usługa publikuje wiadomości, które mogą być odbierane przez wiele innych usług.

---
***Podstawowe pojęcia w RabbitMQ***

**Exchange (Wymiennik)** - Punkt wejścia dla wiadomości w RabbitMQ. Decyduje, do której kolejki trafi wiadomość, na podstawie klucza routing i typu wymiennika.
**Typy wymienników**: 
- *Direct Exchange* - wysyła wiadomości do kolejki z dokładnym dopasowaniem klucza routingu.
- *Fanout Exchange* - wysyła wiadomości do wszystkich kolejek powiązanych z wymiennikiem.
- *Topic Exchange* - wysyła wiadomości do kolejek na podstawie wzorca klucza routingu (np. `order.created`).
- *Headers Exchange* - decyzja na podstawie nagłówków wiadomości.

**Queue (Kolejka)**
Miejsce, w którym wiadomości czekają na przetworzenie przez konsumentów. Kolejki są FIFO (First In, First Out), chyba że skonfigurowane inaczej.

**Binding (Powiązanie)**
Łączy wymiennik z kolejką, definiując zasady routingu.

**Message (Wiadomość)**
Informacja, która jest przesyłana przez RabbitMQ. Składa się z nagłówka - Metadane wiadomości i treści - dane do przetworzenia.

**Channel (Kanał)**
Lekkie połączenie z RabbitMQ używane do komunikacji. Jeden klient może mieć wiele kontaktów.
