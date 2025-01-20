Buffered Streams w IO Javy to zaawansowane strumienie, które poprawiają wydajność operacji odczytu i zapisu, szczególnie w przypadku dużych ilości danych. Wykorzystują one wewnętrzny bufor do przechowywania danych tymczasowo, co minimalizuje liczbę bezpośrednich operacji na źródle danych, takich jak sieć czy pliki.

Wyobraź sobie, że nalewasz wodę z kranu do dużej beczki:
- Jeśli próbujesz napełnić beczkę kropla po kropli, trwa to bardzo długo, bo każda kropla to osobna operacja.
- Lepszym rozwiązaniem jest użycie kubka: nabierasz wodę do kubka, a potem wlewasz ją do beczki większymi porcjami. To zmniejsza liczbę operacji "nabierania".

Buffered Streams w Javie działają dokładnie w ten sposób:
- Dane są tymczasowo przechowywane w **buforze (pamięci pośredniej)**, co pozwala odczytywać lub zapisywać większe porcje danych naraz.
- Dzięki temu program nie musi *wchodzić do pliku* za każdym razem po jeden bajt lub znak - wystarczy jedno wejście, aby pobrać porcję danych do bufora.

***Dlaczego buforowanie jest przydatne?***
Operacje na plikach, sieci, czy innych zasobach zewnętrznych są stosunkowo wolne. Bez buforowania każda operacja odczytu/zapisu wymagałby: Dostępu do systemu operacyjnego i wykonywania czasochłonnych operacji na fizycznym urządzeniu (np. dysku).

Buffered Streams redukują tę liczbę operacji: Zamiast pracować z pojedynczymi bajtami/znakami, operują na większych blokach danych. Operacje na buforze pamięci są dużo szybsze niż operacje bezpośrednio na pliku.


| Nazwa                | Co robi                                       | Pracuje z    |
| -------------------- | --------------------------------------------- | ------------ |
| BufferedInputStream  | Buforuje odczyt danych bajtowych              | InputStream  |
| BufferedOutputStream | Buforuje zapis danych bajtowych               | OutputStream |
| BufferedReader       | Buforuje odczyt danych tekstowych (znakowych) | Reader       |
| BufferedWriter       | Buforuje zapis danych tekstowych (znakowych)  | Writer       |
**Jak działa buforowanie?**
Bufory to nic innego jak tablice w pamięci, które przechowują porce danych.
Podczas odczytu:
 - Dane z pliku są pobierane w blokach i przechowywane w buforze.
 - Program odczytuje dane bezpośrednio z bufora (szybsze, bo w pamięci).
 Podczas zapisu:
 - Pogram zapisuje dane do bufora.
 - Gdy bufor jest pełny, cała jego zawartość jest jednorazowo zapisywana do pliku.