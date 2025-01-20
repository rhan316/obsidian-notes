**Observable** to obiekt, który emituje dane do obserwatorów (ang. Observers).
Jest jak kran z wodą - kiedy ktoś odkręca kran (obserwator się zapisuje), zaczyna lecieć woda (dane).

```
Observable<String> observable = Observable.just("Hello", "RxJava");
observable.subscribe(System.out::println);
```

**Flowable** działa podobnie do *Observable*, ale z obsługą tzw. **blackpressure (mechanizmu regulującego ilość danych w strumieniu, aby uniknąć przeciążenia)**.
Wyobraź sobie to jako zbiornik na wodę w systemie hydraulicznym - jeśli odbiorca nie nadąża z pobieraniem, Flowable ogranicza emisję danych.

*Emituje* odnosi się do procesu, w którym obiekt typu `Observable` (lub inny podobny obiekt jak `FLowable` , `Single` itd.) dostarcza dane do swoich obserwatorów (ang. Observers). Wyobraź sobie to jako przekazywanie wiadomości, wysyłanie sygnałów, czy dostarczanie paczek - każde "emitowanie" to moment, w którym coś jest "przesyłane" w ramach strumienia danych.