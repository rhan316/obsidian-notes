Apache Kafka to system przetwarzania danych oparty na modelu~={10} pub/sub (publisher-subscriber)=~, który jest używany do przetwarzania strumieniowego dużych ilości danych w czasie rzeczywistym. W połączeniu z Javą i frameworkiem Spring, Kafka staje się potężnym narzędziem do budowy nowoczesnych aplikacji przetwarzających dane.

Wyobraź sobie bibliotekę, która działa jak "poczta przyszłości". Ludzie w tej bibliotece (producenci) dostarczają wiadomości (dane) do różnych półek z kategoriami (tematy, ang. topics). Inni ludzie (konsumenci) przychodzą do tej biblioteki i przeszukują wybrane półki, aby odebrać wiadomości, które ich interesują.

~={10}**Topic**=~ = To taka "półka w bibliotece". Wszystkie wiadomości o określonym temacie są przechowywane w jednym miejscu.

~={10}**Producer**=~ = To ktoś, kto dodaje wiadomości do półek. Np. system rejestrujący zamówienia w sklepie internetowym może wysyłać każde zamówienie jako wiadomość do półki o nazwie `orders`.

~={10}**Consumer**=~ = To ktoś, kto odbiera wiadomości z półek. Np. system wysyłający powiadomienia o zamówieniach może odczytywać dane z półki `orders`.

Kafka działa na zasadzie logu, czyli uporządkowanego dziennika zdarzeń. Producent dodaje nowe wpisy, a konsumenci odczytują je w kolejności chronologicznej.

---
Kafka składa się z kilku kluczowych komponentów:

~={10}**Broker**=~ = To "zarządca biblioteki", który przechowuje wiadomości i pilnuje, aby były dostępne dla konsumentów. Broker odpowiada za dystrybucję danych między różnymi serwerami.

~={10}**Partition**=~ = Każdy *topic* jest dzielony na mniejsze części zwane partycjami. Dzięki temu Kafka może skalować się na wiele serwerów, przetwarzają ogromne ilości danych równolegle.

~={10}**Offset** =~= To numer, który przypisuje się każdej wiadomości w partycji. Konsument może dzięki temu wiedzieć, które wiadomości już odczytał, a które jeszcze czekają.

~={10}**Zookeeper**=~ = To "sekretarz biblioteki", który dba o to, żeby brokerzy wiedzieli, gdzie są partycje i jakie są ich stany. W nowszych wersjach Kafki funkcje Zookeepera są stopniowo zastępowane przez wewnętrzne mechanizmy Kafki.

---
Java świetnie współpracuje z Kafką dzięki istniejącym bibliotekom, takimi jak `KafkaProducer` i `KafkaConsumer`.
1. **Producent danych** = Tworzysz aplikację w Javie, która zbiera dane (np. logi, zdarzenia użytkownika, transakcje) i przesyła je do Kafki.
2. **Konsument danych** = Aplikacja odczytuje dane z Kafki i wykonuje na nich jakieś operacje, np. przetwarza transakcje finansowe.
3. **Obsługa dużych wolumenów danych** = Kafka pozwala aplikacjom Java przetwarzać miliony zdarzeń na sekundę w sposób niezawodny.

Framework Spring ma moduł o nazwie Spring for Apache Kafka, który upraszcza integrację Kafki z aplikacjami Java.
1. **Konfiguracja** - Spring pozwala skonfigurować Kafkę za pomocą prostych plików konfiguracyjnych i adnotacji.
```
@KafkaListener(topics = "orders", groupId = "order-service")
public void processOrder(String message) {
	print("Received order: + message);
}
```
2. **Zarządzanie wielowątkowością** - Spring automatycznie zarządza wieloma konsumentami i przetwarzaniem wiadomości, dzięki czemu aplikacja jest bardziej skalowalna.
3. **Obsługa błędów i retry**: Spring Kafka pozwala skonfigurować, co zrobić, gdy przetwarzanie wiadomości się nie powiedzie, np. automatyczne ponawianie próby.
4. **Integracja z innymi komponentami Spring'a** - Możesz łatwo połączyć Kafkę z bazą danych, systemem logowania, czy serwisami REST.

---
**Dlaczego warto używać Kafki?**

1. **Skalowalność** - Dzięki partycjom Kafka może przetwarzać dane na dużą skalę.
2. **Niezawodność** - Kafka przechowuje wiadomości na dysku i pozwala na ich ponowne odczytanie.
3. **Integracja z wieloma systemami** - Kafka łączy różne aplikacje i usługi w jeden spójny ekosystem przetwarzania danych.
4. **Przetwarzanie strumieniowe** - Dzięki bibliotece Kafka Streams możesz utworzyć złożone operacje na strumieniach danych.
