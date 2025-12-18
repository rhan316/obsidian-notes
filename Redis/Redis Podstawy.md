
### Czym jest Redis? (The Core)

Redis (REmote DIctionary Server) to magazyn struktur danych w pamięci operacyjnej (In-Memory).
Działa na jednym wątku (Single-threaded event loop), co eliminuje problemy z lockowaniem zasobów i czyni go absurdalnie szybkim.

#### Kluczowe struktury danych

Jako Java dev musisz wiedzieć, że Redis to nie tylko `String -> String`. Mapujesz te struktury na kolekcje w Javie:

| Struktura Redis | Odpowiednik w Javie       | Zastosowanie                                      |
| --------------- | ------------------------- | ------------------------------------------------- |
| Strings         | `String / byte[]`         | Prosty cache, licznik (INCR/DECR)                 |
| Hashes          | `HashMap<String, String>` | Przechowywanie obiektów (np. profili użytkownika) |
| Lists           | `LinkedList<String>`      | Kolejki zadań (LPUSH/RPOP)                        |
| Sets            | `HashSet<String>`         | Unikalne tagi, systemy rekomendacji               |
| Sorted Sets     | `TreeSet<String>`         | Rankingi (Leaderboards) - każdy element ma score  |
### Persystencja (Bo RAM jest ulotny)

Redis trzyma dane w pamięci, ale może je zapisać na dysku. Masz 2 tryby:
- ***RDB (Snapshotting)***: Co X czasu robi zrzut całej bazy. Szybkie odtwarzanie, ale tracisz dane od ostatniego zapisu.
- ***AOF (Append Only File)***: Loguje każdą operację zapisu. Wolniejsze, ale bezpieczniejsze.
*Zasada*: Na produkcji zazwyczaj używa się obu jednocześnie.

### Integracja ze Spring Bootem

W świecie Springa masz dwie główne drogi:

***A. Spring Cache Abstraction***: Adnotujesz metody, a Spring sam dba o cache. Zero boilerplate.
```java
@Cacheable(value = "users", key = "#id")
public User findById(Long id) { ... }
```

***B. RedisTemplate***: Kiedy potrzebujesz pełnej kontroli nad strukturami (np. chcesz użyć Sorted Sets)
```java
@Autowired
private RedisTemplate<String, Object> template;

public void saveToSet(String key, String value) {
	template.opsForSet().add(key, value);
}
```

### Scenariusze bojowe (To powiedz na rozmowie)

- **Cache Aside Pattern**: Najpierw patrzysz na Redisa. Nie ma? Idziesz do bazy (DB), zapisujesz w Redisie i zwracasz.
- **Distributed Locking (Redlock)**: Masz 5 instancji serwisu i tylko jedna może przetworzyć dany raport? Używasz Redisa jako semafora.
- **Session Management**: Spring Session automatycznie przenosi `HttpSession` do Redisa. Dzięki temu restart serwisu nie wylogowuje użytkowników.

### Eksmisja danych (Eviction Policies)

Kiedy pamięć się kończy, Redis musi coś wyrzucić. Najważniejszy dla ciebie to **LRU (Least Recently Used)** - wywala to, czego nikt dawno nie dotykał. **TTL (Time To Live)** to twój obowiązek - każdy klucz w cache POWINIEN mieć czas wygaśnięcia.

### TL;DR Polski

- Co to = Baza in-memory (RAM), mega szybka, jednowątkowa
- Po co = Cache, sesje, blokady rozproszone, kolejki
- Java = Używasz bibliotek Jedis lub Lettuce (Spring Boot domyślnie używa Lettuce)
- Spring = `@Cacheable` dla wygody, `RedisTemplate` dla precyzji
- Pamiętaj = Zawsze ustawiaj TTL, bo zapchasz RAM i produkcja padnie

### TL;DR English

- What = Single-threaded, In-memory data source
- Use cases = Caching, session store, distributed locks, leaderboards
- Java stack = Lettuce (default in Spring) or Jedis
- Spring = Use `@Cacheable` for abstraction or `RedisTemplate` for advanced data structure manipulation
- Pro tip = Always define an eviction policy (like LRU) and set TTL on keys to prevent OOM (Out Of Memory) errors.


