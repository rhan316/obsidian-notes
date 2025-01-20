
***1. Pisanie kodu źródłowego***
Programista tworzy kod źródłowy w Javie w plikach z rozszerzeniem `.java`. Każda klasa lub interfejs jest zazwyczaj umieszczony w osobnym pliku.

***2. Kompilacja do kodu bajtowego***
Plik `.java` jest przetwarzany przez kompilator Javy (`javac`), który tłumaczy kod źródłowy na kod bajtowy, zapisany w plikach `.class`.

`javac HelloWorld.java`
*Wynik:* Powstaje plik `HelloWorld.class`, który zawiera kod bajtowy (`bytecode`) czytelny dla maszyny wirtualnej Javy (JVM).

***3. Uruchamianie na maszynie wirtualnej Javy (JVM)***
Plik `.class` jest uruchamiany prze JVM, który tłumaczy kod bajtowy na instrukcje maszynowe specyficzne dla danego systemu operacyjnego.

***4. Wykorzystanie Class Loader***
Podczas uruchamiania JVM używa mechanizmu **Class Loader** do ładowania plików `.class` do pamięci. Klasy mogą być ładowane z różnych źródeł, np. z lokalnego systemu plików, archiwów `.jar`, czy przez sieć.
**Etaty ładowania:**
1. *Loading* - ładowanie klasy do pamięci
2. Linking - weryfikacja, przygotowanie i rozdzielenie symboli
3. Init - Inicjalizacja zmiennych statycznych i bloków statycznych w klasie

***5. Interpretacja i kompilacaj Just-In-Time (JIT)***
Kod bajtowy jest początkowo interpretowany prze JVM. Aby poprawić wydajność, JVM wykorzystuje kompilator JIT (Just-In-Time), który tłumaczy najczęściej wykonywane fragmenty kodu bajtowego na natywny kod maszynowy.

***Wykonywanie programu***
Kod maszynowy generowany prze JIT jest wykonywany na procesorze. JVM zarządza także:
1. *Pamięcią* - Garbage Collector zarządza usuwaniem nieużywanych obiektów
2. *Bezpieczeństwem* - weryfikuje kod bajtowy, aby zapewnić jego bezpieczeństwo
3. *Wielowątkowością* - zarządza wątkami aplikacji