Wzorzec *Obserwator* jest jednym z najbardziej klasycznych wzorców projektowych, należącym do ~={red}grupy wzorców behawioralnych.=~ Jego główna idea to umożliwienie jednemu obiektowi (nazywanemu *obserwowanym*, ang.`Subject`) powiadamiania wielu innych obiektów (*obserwatorzy ang. observers*) o zmianach swojego stanu.

***Obserwator jako system subskrypcji wiadomości***
~={orange}~={8}*Obserwowany*=~=~ to serwis wiadomości, który publikuje artykuły.
~={cyan}*Obserwatorzy*=~ to użytkownicy zapisani na newsletter - otrzymują powiadomienia, gdy pojawi się nowy artykuł.
Kiedy serwis (obserwowany) opublikuje nowy artykuł, automatycznie wysyła powiadomienia do wszystkich użytkowników (obserwatorów). Jeśli nowy użytkownik zapisze się na newsletter, od tego momentu również będzie otrzymywał powiadomienia.

**Kluczowe elementy wzorca Obserwator**

1. ***Subject (Obserwowany)*** Obiekt, który posiada listę obserwatorów. Udostępnia metody umożliwiające: dodanie obserwatorów, usuwanie obserwatorów, powiadamianie obserwatorów o zmianie stanu.
2. **Observer (Obserwator)** Obiekt, który rejestruje się u obserwowanego. Implementuje metodę np. `update()`, którą obserwowany wywołuje, gdy coś się zmienia.

```
Diagram UML wzorca Obserwator

+----------------+       +------------------+
|    Subject     |       |    Observer      |
+----------------+       +------------------+
| + attach()     |<>---->| + update()       |
| + detach()     |       +------------------+
| + notify()     |
+----------------+

```