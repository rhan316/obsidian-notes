Java NIO (New Input/Output) to zestaw klas i interfejsów wprowadzonych w Javie 1.4, który uzupełnia starsze klasy I/O (znane jako Java IO). NIO jest zaprojektowane z myślą o większej wydajności i elastyczności, zwłaszcza w aplikacjach, które potrzebują:
- **Nieblokującego wejścia/wyjścia**.
- **Operacji asynchronicznych**.
- **Efektywnego przetwarzania dużych ilości danych**.

***Kluczowe komponenty NIO***
Aby zrozumieć NIO, wyobraź sobie świat kabli, gniazdek elektrycznych i urządzeń:

**Kanały (Channels)** - To jak kable, przez które przepływa prąd (dane). Kanały to ścieżki, którymi dane mogą być przesyłane w obie strony.

**Bufory (Buffers)** - Zbiornik na wodę podłączone do kabla. Dane są tymczasowo przechowywane w buforach, zanim zostaną przetworzone.

**Selektory (Selectors)** - To jak rozdzielacze prądu. Selektory pozwalają jednemu wątkowi zarządzać wieloma kanałami.


| Cecha        | IO                                         | NIO                                         |
| ------------ | ------------------------------------------ | ------------------------------------------- |
| Tryb pracy   | Blokujący (synchronizacja)                 | Nieblokujący (asynchroniczność)             |
| Efektywność  | Jeden wątek na jedno połączenie            | Jeden wątek może obsługiwać wiele połączeń  |
| Model danych | Strumienie (Streams)                       | Bufory (Buffers) i Kanały (Channels)        |
| Wydajność    | Mniejsza w przypadku dużej liczby operacji | Większa przy wielu jednoczesnych operacjach |


