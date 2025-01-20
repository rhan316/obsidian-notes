`Class<?>` w Javie to obiekt reprezentujący klasę lub interfejs w czasie działania programu (runtime). Jest kluczowy element mechanizmu refleksji i dynamicznego zarządzania kodem.

*Kluczowe cechy `Class<?>`

1. **Reprezentuje klasę lub interfejs**: Instancję klasy `Class` opisują strukturę klasy: nazwy, metody, pola, konstruktory. Dostęp do klasy uzyskujesz za pomocą np. Main.class
2. **Generyczność** `<?>` oznacza, że obiekt `Class` może reprezentować dowolny typ. Np. `Class<String>` dla klasy String.
3. **Statyczność** Obiekt `Class` istnieje tylko raz dla każdej załadowanej klasy.
4. **Dynamiczna praca z klasami** Tworzenie instancji klas lub refleksja. Pobieranie metod, pól, konstruktorów. Odczyt i zmiana metadanych klasy.