Reaktywny model programowania to sposób projektowania aplikacji, który koncentruje się na **przepływie danych i zdarzeniach**, zamiast wykonywania krok po kroku, sekwencji poleceń. Kluczowym elementem jest obsługa dużej liczby danych i zapytań w sposób **asynchronicznych i nieblokujący**.

Wyobraź sobie, że zamiast jednego pracownika w restauracji, który gotuje i wydaje zamówienia jedno po drugim (model sekwencyjny), masz system, w którym wiele osób równocześnie przygotowuje różne składniki. Kiedy klient zamawia danie, składniki są dostarczane od razu, gdy są gotowe, a szef kuchni tylko scala jest w całość (reaktywny model).

***Kluczowe elementy reaktywnego modelu**

| Cecha                                     | Opis                                                                                                                                 | Analogia                                                                                                                          |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| ~={red}Asynchroniczność=~                 | Zamiast czekać na wynik jednej operacji przed rozpoczęciem kolejnej, możesz działać niezależnie. Wynik przyjdzie, gdy będzie gotowy. | Zamawiasz pizzę przez telefon. Nie czekasz w pizzerii - robisz inne rzeczy, a dostawca przywozi pizzę, gdy jest gotowa.           |
| ~={green}Nieblokowanie=~                  | Żaden wątek nie jest "blokowany", czekając na odpowiedź. System może obsługiwać wiele operacji równocześnie.                         | W restauracji kucharze nie stoją bezczynnie, czekając, aż ugotuje się ryż - zajmują się innymi potrawami.                         |
| ~={yellow}Przepływ zdarzeń=~              | Wszystko jest obsługiwane jako strumień zdarzeń, np. nowa odpowiedź HTTP, aktualizacja danych w bazie czy kliknięcie użytkownika.    | To jak zlewanie wody do naczynia - woda (zdarzenia) płynie w czasie rzeczywistym, a Ty możesz przechwycić ją w dowolnym momencie. |
| ~={8}Backpressure (regulacja przepływu)=~ | Gdy dane napływają zbyt szybko, system może je ograniczyć lub dostosować tempo przetwarzania.                                        | Jeśli dostarczysz za dużo zamówień naraz do kuchni, szef kuchni powie, żebyś chwilę poczekał, zanim przyjmie kolejne.             |
***Mono i Flux - dwie podstawowe jednostki reaktywne***
W reaktywnym programowaniu w Javie (np. Spring WebFlux) dane przepływają przez **Publisher (wydawcę)**, który jest jak dostawca danych. Publisher w świecie Spring może być reprezentowany przez dwie kluczowe klasy:
1. ==Mono - obsługuje jeden element danych lub rak danych==. Zamawiasz pizzę przez aplikację. Dostajesz pizzę (jeden wynik), albo informację, że jest niedostępna (brak wyniku).
2. ==Flux - obsługuje wiele elementów danych (strumień), który może być skończony lub nieskończony.== Flux to jak oglądanie meczu piłkarskiego na żywo, gdzie wydarzenia (np. bramki) przychodzą w czasie rzeczywistym. Nie wiesz, ile ich będzie, aż mecz się skończy.

***Jak działają Mono i Flux***
Mono służy do obsługi pojedynczych wyników, np. odpowiedzi z API lub wyniku zapytania do bazy danych.
```
Mono<String> mono = Mono.just("Hello, World!");
mono.subscribe(System.out::println);
```
Tworzysz Mono z zawartością "Hello, World!". Subskrybujesz Mono, co powoduje, że wynik zostaje wyświetlony w konsoli. 
Mono może reprezentować także brak wyniku:
```
Mono<String> emptyMono = Mono.empty();
emptyMono.subscribe(print); // Nic nie wyświetli
```

**Flux** obsługuje wiele elementów, np. dane przesyłane strumieniowo lub kolekcję wyników.
```
Flux<String> flux = Flux.just("A", "B", "C");
flux.subscribe(print);
```
```
Flux<Integer> flux = Flux.range(1, 5);
flux.subscribe(print);
```

***Reaktywne strumienie - jak działają w tle?***
Pod maską Mono i Flux korzystają z **Reactive Streams API**, które działa na zasadzie:
- *Publisher* Wydawca danych (np. Mono lub Flux).
- *Subscriber* Konsument danych, który subskrybuje Publisher'a.
- *Subscription* Mechanizm zarządzania strumieniem danych (np. ile danych ma zostać dostarczone jednocześnie).
- *Backpressure* Mechanizm kontrolowania szybkości dostarczania danych.