VTD to koncept struktury danych, w której nie tworzysz obiektów reprezentujących tokeny, tylko zapisujesz informacje o tokenach jako indeksy wskazujące fragmenty oryginalnego bufora danych.

##### Co zwykle robi klasyczny parser JSON?
Typowy parser (Gson, Jackson, org.json):
- czyta JSON
- tworzy obiekty reprezentujące dane
```java
new JsonString("Hello")
new JsonNumber(123)
new JsonObject(...)
```
*To kosztowna operacja - parser musi alokować obiekty, kopiować stringi, buforować liczby itd.*

##### Co robi VTS?
Nie tworzy obiektów.
Nic nie kopiuje z bufora.
Zamiast tego zapisuje adres fragmentu oryginalnego tekstu.

***Tokenu nie przechowujesz jako obiekt, tylko jako:***
- *startIndex* -> gdzie token zaczyna się w tekście
- *length* -> ile znaków zajmuje
- *type* -> jaki to typ(string, number, colon, bracket, itd.)
```ini
position = 123
length = 5
type = STRING
```
I to wszystko. Żadnych obiektów typu `Token`

##### Jak to działa praktycznie?

Załóżmy, że oryginalny JSON to:
```json
{"name": "Jan", "age": 30}
```
Tokenizer znajduje token `"name"` i zapisuje tylko:
```ini
pos = 2
len = 4
type = STRING
```
Cały string `name` dalej siedzi w oryginalnym buforze znaków - bez kopiowania.

##### Dlaczego to jest takie szybkie?

*Zero-copy* -> Nie tworzysz nowych stringów ani obiektów.
*Minimalna ilość alokacji* -> zamiast 1_000 tokenów -> 1_000 obiektów, masz tylko 3 tablice:
- `int[] pos`
- `int[] len`
- `byte[] type`
*Dostęp do danych bezpośrednio z bufora*
```java
string porównujesz bez jego tworzenia:
isEqualUnencoded("name")

VS normalnie:
token.equals("name")
```