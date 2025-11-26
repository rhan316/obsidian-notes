### Co to są tokeny?

Token = najmniejszy znaczący kawałek teksu, który ma sens w języku.
```java
W JSON przykładowe tokeny to:
`{` -> LEFT_BRACE
`}` -> RIGHT_BRACE
`[` -> LEFT_BRACKET
`"name"` -> STRING
`123` -> NUMBER
`true` -> BOOLEAN
```
Tokeny NIE są jeszcze strukturą JSON - to tylko "klocki", z których później parser zbuduje obiekty i tablice.

### Po co w ogóle są tokeny?

Łatwiej analizować dane, gdy są podzielone.
Bardzo trudno jest analizować surowy tekst znak po znaku i rozumieć struktury w locie.
Bardzo łatwo jest dostać strumień tokenów `{ | "name"| : | "Jan" | , | "age" | : | 30 | }`
Potem parser tylko:
- oczekuje klucza -> musi być STRING
- oczekuje dwukropka -> musi być COLON
- oczekuje wartości -> STRING, NUMBER, BOOLEAN...
Dzięki temu logika parsera jest prostsza o rząd wielkości.

### Co to jest tokenizer?

Tokenizer to urządzenie tnące tekst JSON na tokeny.
```json
Wejście (string JSON):
{ "name": "Jan", "age": 30 }

Wyjście (tokeny):
{          → LEFT_BRACE
"name"     → STRING
:          → COLON
"Jan"      → STRING
,          → COMMA
"age"      → STRING
:          → COLON
30         → NUMBER
}          → RIGHT_BRACE
```
Tokenizer:
- czyta tekst znak po znaku
- wykrywa, jaki token zaczyna się w tym miejscu
- liczy długość tokenu
- oznacza jego typ
- zwraca pozycje i długość (VTD!)

## Co to są tokeny w Twoim parserze (VTD)?

U Ciebie tokeny są wirtualne - nic nie kopiujesz, nic nie tworzysz.
Token = (pos, len, type) w oryginalnym buforze.
Np.
String `"name"` w JSON zaczyna się na indeksie 2 i kończy się na 7:
```lua
01234567890123456789
{ "name": "Jan" }
   ^---^
   2    7
```
Toke zapisujemy jako:
```ini
pos = 2
len = 6
type = STRING
```
A jego treść to nie nowy obiekt String, tylko:
```java
data.slice(pos, pos + len)
```
