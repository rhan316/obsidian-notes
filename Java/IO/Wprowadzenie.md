Wyobraź sobie, że komputer to zamknięta skrzynka, w której dzieje się cała logika programu. Jednak ta skrzynka musi się jakoś komunikować z:
- Ludźmi - np. przez klawiaturę, myszkę, ekran czy pliki.
- Z innymi maszynami - np. przez sieć.
- Z innymi programami - np. wymieniając dane między różnymi procesami.
==To właśnie IO jest mostem między tym, co się dzieje wewnątrz programu, a tym, co się dzieje na zewnątrz.==

**Dlaczego IO jest kluczowe w programach?**
1. ~={magenta}Przetwarzanie danych z zewnątrz=~: Np. Twoja aplikacja odczytuje plik CSV, żeby wyświetlić dane użytkownika.
2. ~={yellow}Przechowywanie danych=~: Np. Aplikacja zapisuje wynik obliczeń do pliku tekstowego lub bazy danych.
3. ~={green}Komunikacja=~: Np. Klient poczty e-mail łączy się z serwerem, wysyła dane (output) i odbiera odpowiedzi (input).
4. ~={red}Interakcja z użytkownikiem=~: Np. Gra komputerowa odbiera klawisze naciskane przez gracza (input) i wyświetla animacje na ekranie (output).

**Jak IO działa w Javie?**
Java dostarcza mechanizmów IO, które są podzielone na:
1. **Strumienie (Streams)** - do pracy z ciągłym przepływem danych:
	- *InputStream* - Odczyt danych (np. z pliku lub klawiatury).
	- *OutputStream* - Zapis danych (np. do pliku lub konsoli).
2. **Czytniki i pisarze (Readers/Writers)** - specjalnie dla danych tekstowych:
	- *FileReader/FileWriter* - Praca z plikami tekstowymi.
3. **Buforowane strumienie (Buffered Streams)** - dla szybszej obsługi dużych danych.
4. **Kanały i bufory (NIO)** - bardziej wydajne sposoby zarządzania IO w nowoczesnych aplikacjach.

**Dlaczego IO jest takie ważne?**
Programy bez IO byłyby jak rozmowa do ściany - nie mogłyby odbierać informacji ani ich przekazywać. Dzięki IO programy mogą: Odczytywać dane użytkownika, przechowywać dane, łączyć się z innymi komputerami.

