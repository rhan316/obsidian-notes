Lock to interfejs, który zapewnia kontrolę nad dostępem do zasobu w sytuacjach współbieżnych. Główne implementacje Lock w Javie to:
1. `ReentrantLock` - podstawowa implementacja Lock.
2. `ReentrantReadWriteLock` - zaawansowana implementacja pozwalająca na oddzielenie odczytów i zapisów.

Lock działa podobnie jak `synchronized`, ale oferuje dodatkowe możliwości.

***Jak działa Lock?***

Kluczowe metody interfejsu `Lock`:
1. `lock()` - Blokuje zasób - wątek, który uzyskał blokadę, może kontynuować, inne muszą czekać.
2. `unlock()` - Zwalnia blokadę - pozwala innym wątkom uzyskać dostęp do zasobu.
3. `tryLock()` - Próbuje uzyskać blokadę bez czekania w nieskończoność. Zwraca `true`, jeśli blokada została uzyskana, albo `false`, jeśli nie.
4. `tryLock(long timeout, TimeUnit unit)` - Próbuje uzyskać blokadę w określonym czasie.
5. `lockInterruptibly()` - Blokuje wątek, ale pozwala go przerwać, jeśli wątek jest oczekiwany zbyt długo.


| Cecha                            | synchronized                        | Lock                                                     |
| -------------------------------- | ----------------------------------- | -------------------------------------------------------- |
| Nadmiarowe możliwości            | Ograniczone - działa automatycznie. | Elastyczne - więcej opcji dla programisty.               |
| Próba uzyskania blokady          | Brak - zawsze czeka na wątek        | `tryLock()` pozwala na próbę uzyskania blokady.          |
| Zwolnienie blokady               | Automatycznie (po wyjściu z bloku)  | Musisz ręcznie wywołać `unlock()`                        |
| Obsługa przerwań                 | Nie obsługuje przerwań              | `lockInterruptibly()` pozwala przerwać oczekujący wątek. |
| Wydajność w odczytach i zapisach | Brak rozdzielenia odczytu/zapisu    | `ReentrantReadWriteLock` umożliwia współdzielony odczyt  |
| Obsługa timeoutu                 | Nie obsługuje timeoutu              | `tryLock(timeout)` obsługuje timeout                     |

