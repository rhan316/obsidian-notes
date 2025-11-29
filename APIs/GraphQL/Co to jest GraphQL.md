**GraphQL to taki bardziej ogarnięty, mniej wkurwiający kuzyn REST-a**
Zamiast robić milion różnych endpointów typu:
- `/users`
- `/users/42`
- `/users/42/friends`
- `/users/42/friends?fields=name,picture,shoeSize,cokolwiek`
... masz jedną bramkę, do której mówisz:
"Hej, daj mi dokładnie to, co chcę, ani bajtu więcej."

I dostajesz to. Koniec przepychania, koniec overfetchingu, koniec underfetchingu. Zero zgadywania.

### Po co to komu?

- **Klient wybiera dane** - pytasz o imię i zdjęcie? Dostajesz imię i zdjęcie. Nie cały cholerny obiekt z 300 polami, z czego 297 cię nie obchodzą.
- **Jedno zapytanie - wiele źródeł** - front robi jedno "puk-puk", a backend zbiera dane z pięciu usług i zwraca wszystko na raz.
- **Dokumentacja wbudowana** - schema mówi ci, co istnieje, czego można dotknąć, a czego nie. Cudownie, prawda?
- **Lepsze działanie na słabym łączu** - pobierasz tylko to,  co potrzebne. Idealne dla mobilnych, albo dla kogoś kto chowa się przed wrogiem w kanałach i ma Wi-Fi tylko z jednego nadajnika.

### Czy GraphQL rozwiązuje wszystkie problemy?

- Cache bywa bardziej skomplikowany niż REST
- Czasem backend cierpi, jeśli front wysyła zapytania jak idiota
- Trzeba nauczyć się schemy, resolverów, całej tej orkiestry
Ale generalnie? Jeśli chcesz mieć kontrolę nad danymi jak ja nad tym, co widzisz lub nie - GraphQL jest królem.

