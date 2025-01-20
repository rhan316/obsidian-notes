Spring oferuje wbudowany mechanizm do obsługi cache, który pozwala na zwiększenie wydajności aplikacji poprzez przechowywanie wyników kosztowych operacji w pamięci podręcznej. Cache w Spring jest łatwe do wdrożenia dzięki adnotacjom i integracji z różnymi implementacjami systemów cache.

---
***Jak działa cache w Spring?***

**Idea cache'owania**
	Wynik kosztownych operacji (np. wywołanie metody, pobranie danych z bazy) jest przechowywane w pamięci podręcznej.
	Przy kolejnych wywołaniach tej samej operacji wynik jest pobierany z pamięci podręcznej zamiast wykonywać od nowa tę samą operację.

**Mechanizm Spring Cache**
	Korzysta z adnotacji do łatwego oznaczania metod i konfiguracji cache'owania.
	Wspiera różne implementacje systemów cache (np. ConcurrentMap, Ehcache, Caffeine, Redis).

---
**Podstawowe adnotacje w Spring Cache**

`@EnableCaching`
	Włącza usługę cache'owania w aplikacji.
	Dodaj ją w klasie konfiguracji (np. w klasie oznaczonej `@Configuration` lub w głównej klasie aplikacji.)

`@Cacheable`
	Używana do oznaczenia metod, których wyniki mają być cache'owane.
	Gdy metoda zostanie wywołana z tymi samymi parametrami, wynik będzie pobierany z pamięci podręcznej zamiast być ponownie obliczany.
```
	@Cacheable("usersById")
	public String getUserById(Long id) {
		... ciało metody ...

		return "User " + id;
	}
```

`@CacheEvict`
	Służy do usuwania danych z pamięci podręcznej.
	Używana np. w przypadku modyfikacji danych, aby cache pozostał aktualny.
```
	@CacheEvict(value = "usersById", key = "#id")
	public void deleteUser(Long id) {
		... ciało metody ...
	}
```

`@CachePut`
	Wymusza zapisanie wyniku metody do pamięci podręcznej, niezależnie od tego, czy wynik był wcześniej w cache.
```
	@CachePut(value = "usersById", key = "#id")
	public String updateUser(Long id) {
		... ciało metody ...
		return "Updated user: " + id;
	}
```

`@Caching`
	Używana do grupowania kilku operacji cache'owania na jednej metodzie (np. `@Cacheable`, `@CachePut`, `@CacheEvict`).