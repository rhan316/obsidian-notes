Wyobraź sobie, że prowadzisz cukiernię, która produkuje różne rodzaje ciast: torty, babeczki, serniki, itd. Zamiast każdorazowo instruować cukiernika, jak dokładnie przygotować każde z tych ciast (czyli jak "skonstruować" obiekt), tworzysz *fabrykę ciast*.

To oddzielenie tworzenia (fabryka) od użytkownika (klienta) to właściwe kluczowa zaleta **Factory Pattern**.

***Problemy, które rozwiązuje Factory Pattern***
1. ~={8}Złożoność tworzenia obiektów=~ - Tworzenie obiektów w Javie może być skomplikowane, zwłaszcza jeśli wymagają one wielu parametrów lub konfiguracji. Fabryka ukrywa tę logikę.
2. ~={green}Elastyczność i łatwa modyfikacja kodu=~ - Jeśli w przyszłości zmieni się sposób tworzenia obiektu (np. dodasz nowy typ ciasta), nie musisz modyfikować kodu klienta - wystarczy zaktualizować fabrykę.
3. ~={red}Zmniejszenie powtarzalności =~- Logika tworzenia obiektów jest scentralizowana, więc nie trzeba jej duplikować w różnych częściach kodu.
4. ~={yellow} Zgodność z zasadami SOLID=~ - Przestrzega zasad takich jak *Single Responsibility Principle* (odpowiedzialność za tworzenie obiektów jest oddzielona od reszty logiki) oraz *Open/Closed Principle* (łatwo dodać nowe typy obiektów bez modyfikowania istniejącego kodu).

***Jak działa Factory Pattern w Javie?***
1. **Interfejs lub klasa bazowa** - Określa ogólny kontrakt (metody, które każdy typ obiektu musi implementować).
2. **Klasy konkretne** - Implementują interfejs lub dziedziczą po klasie bazowej - reprezentują różne typy obiektów.
3. **Fabryka** - Klasa, która decyduje, jaki typ obiektu stworzyć i jak to zrobić, na podstawie danych wejściowych.


***Zalety Factory Pattern***
1. **Ukrycie szczegółów tworzenia obiektu**: Klient nie musi wiedzieć, jak dokładnie stworzyć dany obiekt.
2. **Łatwość rozszerzania kodu**.
3. **Lepsza organizacja kodu**.
4. **Centralizacja logiki tworzenia**.