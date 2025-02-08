Wyobraź sobie, że tworzysz aplikację i chcesz, aby działała w różnych językach, np. po polsku, angielsku czy niemiecku. Zamiast pisać osobną wersję aplikacji dla każdego języka (co byłoby baaardzo czasochłonne i niepraktyczne), chcesz oddzielić teksty wyświetlane w aplikacji (np. komunikaty, przyciski, błędy) od kodu programu.

**Resource Bundle** to coś w rodzaju "szafy" lub "kartoteki", w której przechowujesz te teksty w różnych językach. Dzięki temu możesz łatwo zmieniać język aplikacji, po prostu wybierając odpowiedni plik z tej szafy.

---
**Jak to działa?**
1. **Klucz i wartość** - Resource Bundle przechowuje dane w postaci par klucz-wartość. Klucz to coś w rodzaju etykiety, np. `login.button`, a wartość to tekst wyświetlany użytkownikowi, np. "Zaloguj się".
2. **Różne języki** - Masz osobne pliki dla każdego języka:
	- `messages_en.properties` (dla angielskiego)
	- `messages_pl.properties` (dla polskiego)
	- `messages_de.properties` (dla niemieckiego)
Każdy z tych plików zawiera same klucze, ale różne wartości:
W pliku angielskim - `login.button=Log in`
W pliku polskim - `login.button=Zaloguj się`
W pliku niemieckim - `login.button=Anmelden`
3. **Automatyczne dopasowanie języka** - Gdy aplikacja działa, Java automatycznie wybiera odpowiedni plik w zależności od ustawień języka użytkownika.

---
**Prosta analogia**
Pomyśl o Resource Bundle jak o segregatorze z dokumentami:
Każdy język to osobna teczka w segregatorze.
Na każdej stronie (plik `.properties`) masz listę słówek: klucz (np. `hello.message`) i tłumaczenie w danym języku.
Gdy aplikacja potrzebuje tekstu (np. przycisku "Zaloguj się"), otwiera odpowiednią teczkę (język) i szuka właściwego słówka po kluczu.

---
**Dlaczego to takie ważne?**
Tłumacz może pracować bez znajomości kodu - widzi tylko teksty do przetłumaczenia.
Możesz dodać nowy język, tworząc kolejny plik, bez zmieniania kodu aplikacji.
Twój kod staje się bardziej przejrzysty, bo teksty aplikacji są oddzielone od logiki.

**Jak to wygląda w praktyce w Javie?**
- Tworzysz plik `messages.properties` (dla domyślnego języka)
- Dodajesz wersje plików dla innych języków, np. `messages_pl.properties`
- W kodzie używasz klasy `ResourceBundle`, aby pobierać teksty.

```
main {
// Wybieramy język polski
Locale locale = new Locale("pl", "PL");
ResourceBundle bundle = ResourceBundle.getBundle("messages", locale);

// Pobieramy teksty
String loginButton = bundle.getString("login.button");
print(loginButton);
}
```
