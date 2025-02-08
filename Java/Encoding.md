Wyobraź sobie książkę w języku polskim, która musi zostać wysłana do osoby w USA. Problem? Oni nie rozumieją polskich liter, takich jak ą, ę czy ż. Potrzebujesz systemu, który "przetłumaczy" te litery na coś, co można wysłać (np. liczby czy kody), a następnie odbiorca odczyta te liczby i przywróci polskie litery. Ten proces tłumaczenia nazywa się **kodowaniem znaków (character encoding)**.
**Encoding** to sposób zmiany liter i symboli na liczby, które komputer rozumie. Każdy znak (np, A, ą, @) jest reprezentowany przez konkretny numer.

1 bit = najmniejsza jednostka informacji. Bit to skrót od "binary digit" (cyfra binarna). Może przyjmować dwie wartości `0` lub `1`.
1 bajt = 8 bitów. Zestaw 8 bitów. Dzięki temu bajt może reprezentować wiele różnych kombinacji. W sumie jeden bajt może przechowywać 256 różnych wartości, 2 ^ 8 = 256

---
**Co to jest UTF-8?**
UTF-8 to jeden z najpopularniejszych systemów kodowania znaków. Jest to sposób zapisywania tekstu w formie bajtów (małych liczb, które komputer przechowuje w pamięci).

Używa od 1 do 4 bajtów na znak.
1 bajt dla podstawowych znaków ASCII.
2-4 bajty dla bardziej złożonych znaków, takich jak chińskie znaki, emoji, czy specjalne symbole matematyczne.

Obsługuje prawie wszystkie znaki we wszystkich językach świata (alfabety, emotikony, symbole matematyczne itp.)
Dla popularnych znaków (np. łacińskich, takich jak A czy B) używa mniej miejsca, tylko 1 bajt. Dla bardziej złożonych znaków (np. chińskich czy emotikonów) używa więcej bajtów.
Prawie wszystkie aplikacje i strony internetowe używają UTF-8, bo radzi sobie z różnymi językami w jednym systemie.

---

**Co to jest ASCII?**
ASCII (American Standard Code for Information Interchange) to standard kodowania znaków, który przypisuje każdemu znakowi unikalny numer (kod). Dzięki temu komputer może przechowywać i przetwarzać tekst jako liczby.

*Początkowe założenie*
ASCII został opracowany w latach 60 XX wieku, kiedy komputery działały głównie w języku angielskim.
Zawiera 128 znaków.

*Reprezentacja binarna*
Każdy znak ASCII jest zapisany jako liczba w zakresie od 0 do 127. Ta liczba jest następnie reprezentowana w formie binarnej, co zajmuje 7 bitów (2 ^7 = 128)

| Znak | Kod ASCII | Kod binarny |
| ---- | --------- | ----------- |
| `A`  | 65        | 01000001    |
| `a`  | 97        | 01100001    |
| `!`  | 33        | 00100001    |


---
**Dlaczego encoding jest ważny w Javie?**
W Javie wszystko, co dotyczy tekstu, działa w oparciu o kodowanie znaków. Oto, gdzie encoding się pojawia:
- **Odczyt i zapis plików** - Gdy zapisujesz tekst do pliku (np. `.txt`), Java musi wiedzieć, jakie kodowanie użyć, aby zapisać znaki jako bajty. Gdy odczytujesz plik, Java musi znać kodowanie, aby przekształcić bajty z powrotem na znaki.
- **Strumienie danych (np. sieci)** - Gdy wysyłasz dane tekstowe prze internet, encoding określa, jak tekst zostanie zamieniony na dane binarne.
- **Łańcuchy znaków (`String`)** - Wewnątrz Javy, wszystkie `String` są przechowywane jako **Unicode** (specyficzna forma reprezentowania znaków). Ale gdy zapisujesz je do pliku lub wysyłasz przez sieć, musisz je zakodować (np. w UTF-8).

---

| Cecha                   | ASCII                                                         | UTF-8                                                                   | UTF-16                                                                                                          |
| ----------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Zakres znaków           | 128 znaków (0-127), głównie język angielski i znaki kontrolne | Obsługuje pełny zestaw Unicode (ponad 1, 1 miliona znaków)              | Obsługuje pełny zestaw znaków Unicode                                                                           |
| Rozmiar znaków          | Zawsze 1 bajt na znak                                         | Zajmuje od 1 do 4 bajtów na znak.                                       | Zajmuje 2 bajty dla znaków podstawowego zestawu Unicode i 4 bajty dla znaków po za Unicode (np. chińskie znaki) |
| Efektywność             | Bardzo efektywny dla języka angielskiego (tylko 1 bajt)       | Bardziej efektywny dla tekstu zawierającego główne znaki ASCII          | Bardziej efektywny dla języków używających znaków BMP (np. chiński)                                             |
| Kompatybilność wsteczna | Nie wymaga konwersji jest prosty i pierwotny                  | Kompatybilny z ASCII (pierwsze 128 znaków mają identyczne kody)         | Nie jest kompatybilny z ASCII                                                                                   |
| Popularność             | Stary standard, obecnie rzadko używany samodzielnie           | Dominuje w aplikacjach sieciowych i plikach tekstowych (np. HTML, JSON) | Częściej używany w systemach Windows, Javie i plikach binarnych                                                 |
| Kompleksowość           | Najprostszy - brak obsługi języków innych niż angielski       | Prostszy w implementacji (nie wymaga par surrogatów)                    | Bardziej złożony dla znaków spoza BMP (obsługa par surrogatów)                                                  |
