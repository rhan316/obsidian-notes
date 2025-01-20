**JavaScript jest jednowątkowy** - wykonuje tylko jedno zadanie naraz, ale dzięki pętli zdarzeń może obsługiwać wiele zadań asynchronicznych.

**Microtask queue** - np. `.then` ma wyższy priorytet niż message queue (`setTimeout`).

**Event loop** to mechanizm, który zarządza przepływem zadań między różnymi kolejkami i call stack.


***Analogia: Pracownik biurowy i skrzynka zadań***
Wyobraź sobie, że JS to pracownik biurowy, który może robić tylko jedną rzecz naraz (single-thread). Ten pracownik:
- Ma **stos zadań (call stack)**, gdzie wykonuje kolejne rzeczy.
- Ma **skrzynkę na późniejsze zadania (message queue)**, gdzie trafiają zadania do wykonania później (np. obsługa `setTimeout` lub wyniki `Promise`).

**Problem:** Co zrobić, gdy zadanie trwa długo (np. pobieranie danych z serwera)? Pracownik nie może pozwolić, żeby cała reszta pracy utknęła, więc korzysta z mechanizmu **event loop**, który zajmuje się zarządzaniem tymi zadaniami.

***Kluczowe elementy event loop**
1. ~={magenta}**Call stack (stos wywołań)**=~ to miejsce, w którym JS przechowuje bieżące zadania. Stos działa jak stos talerzy w kuchni: Najpierw wkładasz zadanie na górę. Zawsze ściągasz talerz (zadanie) z samej góry.
2. ~={8}**Web APIs (lub Worker Threads)=~.** Jeśli napotkamy zadanie asynchroniczne, nie jest ono wywoływane na stosie. Zamiast tego trafia do systemowych mechanizmów.
3. ~={green}**Message queue (kolejka zadań)**=~ To miejsce, w którym czekają zadania asynchroniczne (np. callbacki lub Promise). Zadania z kolejki są przesyłane na stos wywołań, gdy **call stack jest pusty**.

**Jak działa event loop?**
Event loop jest prostym mechanizmem, który w kółko sprawdza:
- ==Czy call stack jest pusty?== - Jeśli nie, pętla zdarzeń czeka, aż JS zakończy wykonywanie bieżących zadań.
- ==Czy w message queue jest zadanie do wykonania?== - Jeśli tak, przenosi to zadanie na call stack i wykonuje je.

**Co z Promise?**
Promise działa nieco inaczej, ponieważ używa osobnej kolejki zwanej **microtask queue**. Zadania w microtask queue (np. `.then`, `.catch`) mają wyższy priorytet niż te w message queue.