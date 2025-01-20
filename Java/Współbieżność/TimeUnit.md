`TimeUnit` to *enum* w pakiecie `java.util.concurrent`. Jest używany do reprezentowania jednostek czasu, takich jak sekundy, milisekundy, minuty, godziny, czy dni. Główna zaleta `TimeUnit` to zwiększenie czytelności kodu i precyzji kodu, ponieważ możemy wyraźnie określić jednostki czasu w bardziej intuicyjny sposób.

**Dlaczego `TimeUnit.SECONDS.sleep(5)` jest lepszą alternatywą od `Thread.sleep(5_000)?`**

`Thread.sleep(5_000)` -> Liczba 5000 nie mówi bezpośrednio, jakie to są jednostki czasu. Może to być 5_000 milisekund, mikrosekund lub coś innego, jeśli ktoś nie zna kontekstu. Programista musi wiedzieć, że `Thread.sleep()` używa milisekund.

`TimeUnit.SECONDS.sleep(5)` - Od razu wiadomo, że mówimy o 5 sekundach. `TimeUnit` automatycznie zmienia czas w odpowiednie jednostki, więc unikamy błędów w obliczeniach.

*Konwersja jednostek czasu*
```
long sekundy = TimeUnit.MINUTES.toSeconds(1) ==> 60
long days = TimeUnit.HOURS.toDays(300) ==> 12
```

*Zarządzanie timeoutami*
```
var executor = Executors.newSingleThreadExecutor();

try {
	Funture<String> future = executor.submit(() -> {
		TimeUnit.SECONDS.sleep(2);  // Symulacja opóźnienia
		return "Wynik zadania!";
	});

	// Czekaj maksymalnie 1 sekundę na wynik
	String result = future.get(1, TimeUnit.SECONDS);
}
```

Praktyczne zastosowania `TimeUnit`:

1. **Konwersja jednostek czasu** – unikaj błędów w obliczeniach.
2. **Timeouty** – zarządzaj limitami czasowymi w aplikacjach wielowątkowych.
3. **DelayQueue** – twórz opóźnione zadania w kolejkach.
4. **Timery i odliczanie** – implementuj liczniki i funkcje odliczania.
5. **Ograniczanie operacji** – zarządzaj tempem przetwarzania (rate limiting).
6. **Animacje i symulacje** – kontroluj opóźnienia w precyzyjnych operacjach.
 i inne...