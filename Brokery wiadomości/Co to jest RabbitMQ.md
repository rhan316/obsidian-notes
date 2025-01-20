RabbitMQ to **broker wiadomości (ang. message broker)** - oprogramowanie pośredniczące, które umożliwia aplikacjom wymianę komunikatów w sposób asynchroniczny i zdecentralizowany. Jest to narzędzie do obsługi kolejek wiadomości, które działają zgodnie z modelem **publisher-subscribe i queue-base messaging**. RabbitMQ korzysta z protokołów AMQP (Advanced Message Queuing Protocol) i może być używany w wielu językach, w tym w Javie.

Wyobraź sobie centrum logistyczne:
- **Producent (producent wiadomości)** - wysyła paczki (wiadomości) do centrum dystrybucji (RabbitMQ).
- Centrum przechowuje paczki w odpowiednich strefach (kolejkach).
- Kurierzy (odbiorcy) przychodzą po paczki i dostarczają je do adresatów.

RabbitMQ działa jak to centrum logistyczne:
- Zarządza wiadomościami, zapewniając ich dostarczenie.
- Organizuje komunikację między różnymi systemami, które mogą działać w różnych językach programowania i środowiskach.

---
RabbitMQ rozwiązuje problem **asynchronicznej komunikacji** między systemami. Oto główne zastosowania:

**Asynchroniczne przetwarzanie**: Umożliwia odciążenie głównych procesów aplikacji poprzez delegowanie czasochłonnych zadań do osobnych usług.

**Mikroserwisy**: RabbitMQ umożliwia komunikację między mikroserwisami w architekturze rozproszonej.

**Obsługa kolejek zadań**: Możesz dodawać zadania do kolejki i przetwarzać je w tle, np. generowanie raportów, przetwarzanie obrazów, wysyłanie e-maili.

**Model publish-subscribe**: Jedna usługa publikuje wiadomości, które mogą być odbierane przez wiele innych usług.

---
