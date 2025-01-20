W Javie **Semaphore** znajduje się w pakiecie *java.util.concurrent*. To narzędzie, które ogranicza liczbę wątków, które mogą jednocześnie uzyskać dostęp do określonego zasobu. Jest to szczególnie przydatne, gdy chcesz zapewnić, że tylko określona liczba wątków wykonuje pewną operację w tym samym czasie.

**Jak działa Semaphore?**
1. *Wartość początkowa (permits)* - Gdy tworzysz obiekt `Semaphore`, określasz liczbę "przepustek" (ang. permits). Każda przepustka pozwala jednemu wątkowi uzyskać dostęp do zasobu.
2. *Metoda `acquire()`* - Wątek próbuje uzyskać przepustkę. Jeśli przepustka jest dostępna, wątek ją "bierze" i kontynuuje pracę. Jeśli nie, wątek czeka, aż jakaś przepustka się zwolni.
3. *Metoda `release()`* - Wątek zwalnia przepustkę, oddają ją do puli. 

**Semaphore jako parking**

```
class Parking {
	private final Semaphore sem;

	public Parking(int places) {
		sem = new Semaphore(places) // Liczba miejsc na parkingu
	}

	public void park(String car) {
		print(car + " czeka na miejsce.");
		sem.acquire(); // Próba zajęcia miejsca na parkingu.
		print(car + " zaparkował.");
		Thread.sleep(2000); // Symulacja czasu parkowania

		(...)
		finally {
			print(car + " opuszcza parking");
			sem.release(); // Zwolnienie miejsca
		}
	}
}

public class Main {
	psvm {
		var parking = new Parking(2); // Parking ma tylko 2 miejsca

		for (int i = 1, (...))
			String car = "Samochód " + i;
			new Thread(() -> parking.park(car)).start();
	}
}
```

**Jakie problemy rozwiązuje Semaphore?**

1. *Ograniczenie dostępu do zasobów*: Semaphore jest używany, gdy mamy zasób, do którego dostęp jednocześnie może mieć ograniczona ilość wątków. Przykłady:
	1. Połączenie do bazy danych - kontrola maksymalnej liczby połączeń
	2. Dostęp do plików - ograniczenie liczby procesów czytających ten sam plik
2. *Unikanie przeciążenia:* Gdy masz system, które może obsłużyć tylko określoną liczbę żądań (np. serwer HTTP obsługujący 100 klientów jednocześnie), Semaphore pozwala kontrolować liczbę aktywnych klientów.
3. *Synchronizacja wątków:* Semaphore może być używany do koordynacji wątków, np. upewniając się, że pewne sekcje kodu są wykonywane tylko przez określoną liczbę wątków w danym momencie.