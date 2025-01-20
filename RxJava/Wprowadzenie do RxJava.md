
**Co to jest RxJava?**
RxJava to biblioteka oparta na wzorcu *reaktywnego programowania.* Umożliwia pracę z *asynchronicznymi strumieniami danych,* pozwalając na reagowanie na zmieniające się dane w czasie rzeczywistym.

**Czym jest programowanie reaktywne?**
Wyobraź sobie, że jesteś kelnerem w restauracji. Przyjmujesz zamówienia od klientów i przekazujesz je do kuchni. Nie stoisz przy jednym kliencie, czekając, aż kuchnia przygotuje jego jedzenie. Zamiast tego obsługujesz kolejnych klientów, a kiedy kuchnia skończy gotować, po prostu cię informuje, że posiłek jest gotowy. Dzięki temu możesz obsłużyć wielu klientów na raz, zamiast tracić czas na stanie i czekanie na jedno danie.

*Analogia*

RxJava to system dostarczania wiadomości:
1.~={red} **Observable**=~ to nadawca (ktoś wysyła wiadomości).
2. ~={8}**Observer** =~to odbiorca (ktoś nasłuchuje i reaguje na te wiadomości).
3. ~={magenta}**Operators**=~ to filtry, które mogą modyfikować, filtrować lub przekształcać wiadomości przed ich dostarczeniem.
4. ~={blue}**Schedulers**=~ to kurierzy, którzy zarządzają, gdzie i jak wiadomości są dostarczane (np. w tle, w głównym wątku aplikacji).

***Podstawowe komponenty RxJava***

- ~={red}**Observable (lub Flowable)**=~ - źródło danychh, które emituje zdarzenia. Przykład: Strumień wiadomości, kliknięcia użytkownika, dane z API.
- ~={8}**Observer**=~ - Reaguje na zdarzenia emitowane przez Observable. Reakcja na zdarzenia:
	 1. `onNext` - Kiedy nowe dane są dostępne.
	 2. `onError` - Kiedy wystąpi błąd.
	 3. `onComplete` - Kiedy Observable zakończy zadanie.
- ~={magenta}**Operators**=~ - Transformują lub przetwarzają dane w strumieniu (np. `map`, `filter`, `flatMap`).
- ~={blue}**Schedulers**=~ - Określają, w jakim wątku Observable i Observer będą działać (np. w tle, w głównym wątku).

