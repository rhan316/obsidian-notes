Pakiet `java.time` to nowoczesne API do zarządzania datami, czasem i strefami czasowymi, wprowadzone w Java 8. Został zaprojektowany jako następca starszych klas, takich jak `java.util.Date`, `java.util.Calendar` i `java.util.TimeZone`. Jego celem było uproszczenie pracy z czasem, zwiększenie czytelności kodu i uniknięcie typowych problemów z poprzednim API, takich jak mutowalność i nieintuicyjne operacje.

---
***Kluczowe elementy `java.time`***

Podstawowe klasy do pracy z czasem i datą:

| Klasa           | Opis                                                   | Przykład                               |
| --------------- | ------------------------------------------------------ | -------------------------------------- |
| `LocalDate`     | Reprezentuje datę (bez godziny i strefy czasowej)      | `2025-01-25`                           |
| `LocalTime`     | Reprezentuje czas (bez daty i strefy czasowej)         | `14:30:00`                             |
| `LocalDateTime` | Łączy datę i czas, ale bez strefy czasowej             | `2025-01-25T14:30:00`                  |
| `ZoneDateTime`  | Reprezentuje datę i czas w określonej strefie czasowej | `2025-01-25T14:30:00+01:00[Eu/Warsaw]` |

Klasy do operacji czasowych:
- `Duration`: Reprezentuje odstęp czasu w sec. i nano sec. Np. `PT2H30M` (2 godz. i 30 min.)
- `Period`: Reprezentuje odstęp czasu w dniach, miesiącach lub latach. Np. `P2Y3M` (2 lata i 3 miesiące)

Klasy do stref czasowych:
- `ZoneId`: Identyfikator strefy czasowej. Np. `Europe/Warsaw`.
- `ZoneOffset`: Przesunięcie czasowe od UTC. Np. `+01:00`.

Klasa `Instant` - Reprezentuje punkt w czasie w formacie UTC. Np. `2025-01-25T13:30:00Z`.

Klasa `Clock` - Zapewnia dostęp do aktualnego czasu i daty. Użyteczne w testach, gdy trzeba symulować różne czasy.

---
**Formatowanie i parsowanie**

`DateTimeFormatter` Narzędzie do formatowania i parsowania dat oraz czasów.
Wspiera wzorce niestandardowe (np. `yyyy-MM-dd HH:mm:ss`).
```
var formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
var dateTime = LocalDateTime.parse("2025-01-25 14:30", formatter);
```
