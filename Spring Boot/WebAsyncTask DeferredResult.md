To narzędzia do obsługi asynchronicznych żądań HTTP. Umożliwiają one odciążenie wątku serwera poprzez wykonywanie operacji w tle, co jest szczególnie przydatne w przypadku długotrwałych procesów (np. wywołań zewnętrznych API, przetwarzania danych).

---
***Dlaczego używać asynchronicznego przetwarzania w Spring?***

**Odciążanie wątków serwera** - serwer może zwolnić wątek odpowiedzialny za obsługę żądania i przydzielić go innym zadaniom, podczas gdy asynchroniczne operacje są wykonywane w tle.

**Skalowalność** - w przypadku aplikacji z dużą liczbą równoczesnych żądań (np. REST API), asynchroniczne przetwarzanie pozwala efektywnie zarządzać zasobami.

**Nieblokujące operacje** - pozwala na integrację z systemami zewnętrznymi (np. innymi API, bazami danych) w sposób nieblokujący.

---
**DeferredResult** 
	Obiekt `DeferredResult` służy do obsługi asynchronicznych odpowiedzi HTTP.
	Pozwala zwrócić odpowiedź do klienta w momencie, gdy wynik operacji jest gotowy, bez blokowania wątku serwera.
```
@GetMapping("/")
public DeferredResult<String> getMethod() {
	DeferredResult<String> result = new DeferredResult<>();
	ThreadPool.submit() => TimeUnit.SECONDS.sleep(5);
	result.setResult("Complete!");
}
```

---
**WebAsyncTask**
	`WebAsyncTask` to wyższy poziom abstrakcji niż `DeferredResult`.
	Oferuje prostszą obsługę timeoutów, wyjątków i niestandardowego programowania wątków.
```
	@GetMapping("/s")
	public WebAsyncTask<String> getAsnycTask() {
		WebAsyncTask<String> task = new WebAsyncTask<>(5000L, () -> {
			... working ...
			
		})

		task.onTimeout(() -> "Timeout!");
		task.onError(() -> "Error!");

		return task;
	};
```

---

| Cecha             | DeferredResult                           | WebAsyncTask                                   |
| ----------------- | ---------------------------------------- | ---------------------------------------------- |
| Abstrakcja        | Niskopoziomowe API                       | Wyższy poziom abstrakcji                       |
| Obsługa timeoutów | Musisz samodzielnie obsłużyć timeout     | Obsługa timeoutów za pomocą `onTimeout()`      |
| Obsługa błędów    | Ręczne ustawienie błędu `setErrorResult` | Wbudowana obsługa błędów za pomocą `onError()` |
| Kod               | Wymaga więcej kodu do implementacji      | Bardziej elegancki i czytelny kod              |
