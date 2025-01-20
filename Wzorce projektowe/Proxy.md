Wzorzec projektowy **Proxy (pełnomocnik)** to jeden z tzw. *wzorców strukturalnych*, który umożliwia wstawienie "pośrednika" pomiędzy klienta (czyli kod, który chce coś zrobić) a rzeczywisty obiekt, z którym klient chce współpracować. Proxy działa jak "zastępca", który kontroluje dostęp do właściwego obiektu.

Wyobraź sobie, że chcesz wynająć samochód. Nie idziesz bezpośrednio do parkingu z samochodami, tylko kontaktujesz się z pracownikiem wypożyczalni (proxy), który:
- Sprawdza, czy masz prawo jazdy.
- Upewnia się, że zapłaciłeś kaucję.
- Dopiero potem daje ci dostęp do samochodu.
Ten pracownik to właśnie **Proxy** - kontroluje, kto i na jakich warunkach może uzyskać dostęp do rzeczywistego obiektu (samochodu).

*W Javie Proxy może być zaimplementowane w różnych wariantach:*
1. **Proxy weryfikujący dostęp** - kontroluje, czy użytkownik ma prawo do korzystania z obiektu.
2. **Proxy pamięci podręcznej (caching)** - przechowuje wyniki kosztownych operacji, aby nie trzeba było ich powtarzać.
3. **Proxy zdalne (remote proxy)** - pozwala komunikować się z obiektem znajdującym się w innym systemie (np. na innym serwerze).
4. **Proxy logujące** - zapisuje operacje wykonywane na obiekcie.

***Kluczowe zalety wzorca Proxy***
1. **Kontrola dostępu** - Proxy może sprawdzać, kto i kiedy ma dostęp do rzeczywistego obiektu.
2. **Opóźniona inicjalizacja** - Rzeczywisty obiekt nie jest tworzony, dopóki nie jest naprawdę potrzebny.
3. **Ograniczenia kosztów** - Proxy może buforować wyniki operacji lub unikać zbędnych wywołań zdalnych.