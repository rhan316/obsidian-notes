Executor w Javie to wzorzec projektowy, który służy do zarządzania wykonywaniem zadań w tle w sposób efektywny i uporządkowany. Jest częścią *Java Concurrency API*, która wprowadzona została w wersji Java 5, aby ułatwić pracę z wielowątkowością i równoległością.

Żeby zrozumieć, czym jest Executor, wyobraź sobie kuchnię w resturacji:
1. **Kucharz (wątek)** - Fizyczna jednostka wykonująca zadanie, np. gotowanie dania.
2. **Zamówienie (zadanie)** - Konkretne danie do przygotowania.
3. **Manager kuchni (Executor)** - Osoba organizująca pracę kucharzy. Manager decyduje, kto, kiedy i co ma gotować. Nie gotuje sam, ale rozdziela zamówienia między kucharzy.

**Jak działa Executor?**

W świecie Javy, Executor zajmuje się zarządzaniem wątkami i zadaniami w podobny sposób jak manager kuchni. Gdy masz zadania do wykonania, zamiast samodzielnie uruchamiać nowe wątki (co jest skomplikowane i nieefektywne), przekazujesz te zadania do Executor (Egzekutora). Executor zajmuje się resztą.

**Kluczowe komponenty Executor**

***Interfejs `Executor`***
	Najprostszy interfejs w tej hierarchii.
	Posiada jedną metodę `void execute(Runnable command);`
	Przykład: Wyobraź sobie, że mówisz managerowi kuchni: "Przygotuj pizzę". Manager przypisze to zadanie do wolnego kucharza.

***ExecutorService***
	Rozszerza możliwości zwykłego Egzekutora.
	Pozwala na zarządzanie życiem wątków: uruchamianie, zatrzymanie itp.
	Przykład: Manager kuchni może zamknąć kuchnię na noc lub czekać, aż wszystkie dania zostaną przygotowane.

***ThreadPoolExecutor***
	Najbardziej rozbudowany i konfigurowalny rodzaj Executor
	Pracuje z **pulą wątków** (ang. thread pool). Pula to zestaw kucharzy gotowych do pracy.
	Dzięki temu nie trzeba za każdym razem zatrudniać nowego kucharza - można wykorzystać tych, którzy już są.
	*Możliwości:*
		Ustalanie minimalnej i maksymalnej liczy wątków.
		Określanie, jak długo wątek może być nieaktywny, zanim zostanie zwolniony.
		Kolejkowanie zadań.

***ScheduledExecutorService***
	Rozszerzenie `ExecutorService`, które pozwala na wykonywanie zadań cyklicznie lub z opóźnieniem.
	Przykład: Codzienne przygotowanie raportu w firmie.


**Dlaczego warto używać Executor?**

*Efektywność* - Tworzenie nowych wątków za każdym razem jest kosztowne. Egzekutor z pulą wątków pozwala ponownie wykorzystać już istniejące wątki.
*Łatwiejsze zarządzanie* - Nie musisz ręcznie zarządzać cyklem życia wątków - Egzekutor zajmuje się tym za Ciebie.
*Bezpieczeństwo i porządek* - Dzięki ustandaryzowanemu zarządzaniu wątkami unikasz potencjalnych błędów, np. utraty danych przez niepoprawne zamykanie wątków.

