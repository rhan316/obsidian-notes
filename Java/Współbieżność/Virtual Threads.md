Virtual Threads to nowy rodzaj wątków wprowadzony w ramach projektu Loom w Javie, zaprojektowany w celu uproszczenia programowania współbieżnego i poprawy skalowalności aplikacji. Są lekkimi wątkami zarządzanymi przez JVM, a nie przez system operacyjny, co pozwala na efektywniejsze zarządzanie zasobami w przypadku dużej liczby jednocześnie działających zadań.

***Czym są Virtual Threads?***
	*Definicja:* Virtual Threads to wątki uruchamiane przez JVM, które są abstrahowane od wątków systemowych (OS Threads). W przeciwieństwie do klasycznych wątków (ang. Platform Threads), Virtual Threads nie są na stałe przypisane do wątków OS.
	*Lekkość:* Są lekkie jak obiekty w Javie - ich tworzenie, przełączanie i zarządzanie jest znacznie tańsze niż klasycznych wątków.
	*Skalowalność:* Mogą obsługiwać tysiące, a nawet miliony równoległych zadań, czego nie da się osiągnąć efektywnie za pomocą klasycznych wątków.

***Analogia - restauracja***
*Platform Threads* - Każdy klient (zadanie) dostaje przypisanego na stałe kelnera (wątek OS). Problem pojawia się, gdy liczba klientów rośnie - restauracja potrzebuje coraz więcej kelnerów, co staje się nieefektywne.
*Virtual Threads* - Klienci dzielą kelnerów. Kelner obsługuje klienta tylko wtedy, gdy klient czegoś potrzebuje, a w międzyczasie obsługuje innych klientów.

***Jak działają Virtual Threads?***
*Mechanizm działania*. Wirtualne wątki są mapowane na wątki OS tylko w czasie rzeczywistego wykonywania (gdy aktywnie korzystają z CPU). Jeśli Virtual Thread czeka na operację (np. sieć, pliki), JVM automatycznie wstrzymuje go, zwalniając wątek OS.
*Wykorzystywanie Fork/Join Pool* - Wirtualne wątki współdzielą wątki OS zarządzane prze JVM w ramch Fork/Join Pool.
