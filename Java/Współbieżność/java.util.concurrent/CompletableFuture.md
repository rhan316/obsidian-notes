***Co to jest CompletableFuture?***
Wyobraź sobie, że jesteś w restauracji i składasz zamówienie. Kelner przyjmuje Twoje zamówienie (np. pizze) i przekazuje je do kuchni. Nie musisz stać i czekać, aż pizza będzie gotowa - możesz w tym czasie zrobić coś innego (np. przeglądać menu na deser). Kiedy pizza jest gotowa, kelner przynosi ją do Twojego stołu.
- ~={red}Ty=~ to program, który wykonuje inne zadania.
- ~={red}Pizza=~ to wynik operacji (np. pobieranie danych z serwera).
- ~={red}CompletableFuture=~ to mechanizm, który pozwala Ci otrzymywać powiadomienie, gdy wynik (pizza) będzie gotowy.

**Jak to działa technicznie?**
Najpierw zrozummy, czym jest `Future`, z którego wywodzi się `CompletableFuture`. Future to prosty mechanizm reprezentujący wynik, który będzie dostępny w przyszłości. Wyobraź sobie to jako obietnicę "Dostarczę wynik później".
```
var executor = Executros.newSignleThreadExecutor();
Future<String> future = executor.submit(() -> {
	Thread.sleep(2_000);
	return "Gotowe!";
});

// ... kod ... //
String wynik = future.get(); => "Gotowe!";
```

**CompletableFuture - rozszerzenie możliwości Future**
`CompletableFuture` rozwiązuje te problemy, pozwalając na:
- Rejestrację zadań, które zostaną wykonane, gdy wynik będzie gotowy.
- Łączenie wielu zadań asynchronicznych.
- Obsługę wyjątków w sposób bardziej elegancki.
```
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
	try {
		Thread.sleep(2_000); // Symuluje długotrwałe działanie
	} catch(...) {...}
})
```

**Główne metody CompletableFuture**
`supplyAsync` => Uruchamia zadanie, które zwraca wynik.
`runAsync` => Uruchamia zadanie, które nic nie zwraca (tylko efekt uboczny).
```
// Zwraca wynik
CompletableFuture<String> result = CompletableFuture.supplyAsync(() -> "Hello!");

// Nic nie zwraca
CompletableFuture<Void> task = CompletableFuture.runAsync(() -> print("Hi!"));
```

`thenApply` => Przetwarza wynik i zwraca przekształcony.
`thenAccept` => Przyjmuje wynik, ale nic nie zwraca.
`thenRun` => Uruchamia zadanie, ale ignoruje wynik.
```
CompletableFuture.supplyAsync(() -> "Hi ")
	.thenApply(r -> r + " there!")
	.thenAccept(System.out::println)
	.thenRun(() -> print("End."));
```

`thenCompose` => Łączy dwa asynchroniczne zadania, gdzie drugie zależy od wyniku pierwszego.
`thenCombine` => Łączy dwa asynchroniczne zadania niezależnie i łączy ich wyniki.
```
// thenCompose
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> "Cześć");
CompletableFuture<String> future2 = future1.thenCompose(result -> CompletableFuture.supplyAsync(() -> result + " Świecie!"));
future2.thenAccept(System.out::println);

// thenCombine
CompletableFuture<Integer> liczba1 = CompletableFuture.supplyAsync(() -> 5);
CompletableFuture<Integer> liczba2 = CompletableFuture.supplyAsync(() -> 10);
CompletableFuture<Integer> suma = liczba1.thenCombine(liczba2, Integer::sum);
suma.thenAccept(result -> System.out.println("Suma: " + result));
```

**Obsługa wyjątków**
`CompletableFuture` pozwala elegancko obsługiwać błędy za pomocą metod takich jak:
`exceptionally` - zwraca domyślną wartość w przypadku błędu.
`handle` - obsługuje zarówno wynik, i jak i błąd.
