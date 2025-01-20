Żeby dobrze zrozumieć, dlaczego istnieją interfejsy `Callable` i `Future`, wyobraźmy sobie, że programowanie to życie na farmie, a Ty jesteś farmerem:
*Zadanie (Callable)* to nasionko, które sadzisz w ziemi, żeby wyrosło w przyszłości w coś wartościowego (np. marchewka).
*Rezultat zadania(Future)* to jak kupon do odbioru plonów - pozwala sprawdzić, czy marchewka jest już gotowa do odebrania, a jeśli tak, możesz ją zabrać.

***Problem, który rozwiązują `Callable` i `Future`***
Wcześniej w Javie do uruchomiania kodu w wątkach korzystało się głównie z interfejsu `Runnable`. Ale `Runnable` ma pewne ograniczenia:
1. **Brak wyniku:** `Runnable` nie pozwala zwrócić wartości po zakończeniu zadania. Po prostu wykonuje kod i na tym koniec.
2. **Brak obsługi wyjątków:** Jeśli w zadaniu `Runnable` wystąpi wyjątek, nie masz bezpośredniego mechanizmu, aby go przechwycić.

`Callable` i `Future` rozwiązują te problemy, dodając wsparcie dla zwracania wyników i obsługi wyjątków w zadaniach.


**`Callable` Zadanie zwracające wynik***
`Callable` to ulepszona wersja interfejsu `Runnable`, która pozwala:
- Zwrócić wartość po zakończeniu zadania.
- Rzucić wyjątek podczas wykonania.
	 `V call() throws Exception;`
	 
```
Wyobraź sobie, że sadzisz nasionko marchewki. Po pewnym czasie chcesz sprawdzić, czy plon jest gotowy (wynik), i ewentualnie zobaczyć, czy coś poszło nie tak (np. marchewka nie wyrosła).

public class ExampleCallable implements Callable<String> {
	@Override
	public String call() throws Exception {
		Thread.sleep(2000); // Symulacja pracy

		return "Marchewka gotowa!";
	}
}
```

**`Future` Otrzymywanie wyniku w przyszłości**
`Future` to obiekt reprezentujący wynik zadania, które może jeszcze nie być gotowe.
*Cechy:*
- **Sprawdzenie statusu zadania (czy zostało zakończone).**
- **Pobrać wynik zadania jeśli jest gotowe.**
- **Przerwać zadanie, jeśli nie jest już potrzebne.**

```
Metody `Future`:

boolean cancel(boolean mayInterruptIfRunning); // Anuluje zadanie
boolean isCancelled(); // Sprawdza, czy zadanie zostało anulowane
boolean isDone(); // Sprawdza, czy zadanie się zakończyło
V get(); // Pobiera wynik, blokując wątek, aż wynik będzie gotowy
V get(long timeout, TimeUnit unit) // Pobiera wynik z limitem czasowym
```

***Dlaczego warto korzystać z `Callable` i `Future`?***
1. Zwracanie wyników: Używasz `Callable`, jeśli zadanie musi zwrócić wartość (np. wynik obliczeń, dane z API itp.).
2. Obsługa wyjątków: `Callable` pozwala przechwycić wyjątki bez dodatkowego kombinowania.
3. Asynchroniczność: `Future` umożliwia monitorowanie stanu zadania i odbierania wyniku bez konieczności natychmiastowego czekania.