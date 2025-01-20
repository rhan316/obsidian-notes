Wzorzec projektowy **Obserwator** (obserwator) to jeden z tzw. *wzorców behawioralnych*, który pozwala na implementację mechanizmu powiadamiania o zmianach stanu obiektu w sposób *luźno powiązany* (low coupling). Oznacza to, że obiekt obserwowany nie musi wiedzieć dokładnie, kto go obserwuje ani co obserwator zrobi z otrzymanymi informacjami.

*Analogia*

Wyobraź sobie, że subskrybujesz newsletter w serwisie internetowym. Serwis to obiekt, który wysyła wiadomości (obiekt obserwowany), a ty jesteś jednym z subskrybentów (obserwatorów). Gdy serwis publikuje nowe wiadomości, wysyła je do wszystkich swoich subskrybentów. Ty, jako obserwator możesz zdecydować, co zrobisz z tymi wiadomościami - np. je przeczytasz, zignorujesz, albo zrezygnujesz z subskrypcji.


***Problemy, które rozwiązuje wzorzec Obserwator (Observer)***

1. **Zarządzanie zdarzeniami i powiadomieniami**. Kiedy jeden obiekt zmienia swój stan, wiele innych obiektów może być o tym poinformowanych. Przykład: Zmiana ceny akcji powinna natychmiast powiadomić wszystkie aplikacje monitorujące giełdę.
2. **Odseparowanie obiektów**. Obserwowany nie zna szczegóły implementacji obserwatorów. Przykład: Aplikacja czatu może mieć różne rodzaje klientów (np. aplikacja mobilna, desktopowa), które reagują na nowe wiadomości.
3. **Elastyczność**. Obserwatorzy mogą być dodawani lub usuwani w trakcie działania programu, co zwiększa modułowość i łatwość rozszerzania aplikacji.

