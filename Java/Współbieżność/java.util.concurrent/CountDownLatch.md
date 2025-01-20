Umożliwia synchronizację jednego lub więcej wątków poprzez czekanie na zakończenie pracy innych wątków. Wyobraź sobie, że `CountDownLatch` to taki mechanizm, który działa jak brama - jeden wątek (lub więcej) czeka, aż inne wątki "opuszczą swoje sygnały", czyli wykonają swoje zadania. Dopiero wtedy brama zostaje otwarta i czekające wątki mogę kontynuować.

*Jak działa `CountDownLatch`?
1. Ustawienie początkowej wartości licznika `count`: Gdy tworzysz obiekt `CountDownLatch`, ustawiasz liczbę operacji, na które wątki mają czekać.
2. `await()`: Wątki wywołujące `await()` czekają, aż licznik osiągnie 0. Blokada wątku zostanie zdjęta dopiero wtedy,  gdy wszystkie zadania zostaną ukończone.
3. `countDown()`: Każdy wątek, który kończy swoją pracę, wywołuje `countDown()`. To zmniejsza wartość licznika o 1.
4. Gdy licznik osiągnie 0, wszystkie wątki wywołujące `await()` mogą kontynuować.

*Analogia*

Wyobraź sobie, że masz zespołową grę planszową. Gracze (różne wątki) muszą najpierw rzucić kośćmi i wykonać swoje ruchy (operacje). Dopiero gdy każdy gracz skończy swoją turę, gra może przejść do następnej fazy. `CountDownLatch` czeka, aż wszyscy gracze skończą.

**Zastosowania `CountDownLatch`:
1. *Oczekiwanie na zakończenie pracy wielu wątków*
	- Synchronizacja głównego wątku z podwątkami
	- Scenariusz, gdzie główny wątek musi poczekać na wyniki pracy innych wątków przed kontynuacją
2. *Uruchamianie wielu wątków jednocześnie*: 
	- Możesz zastosować `CountDownLatch` z początkowym licznikiem ustawionym na 1.
	- Wątki czekają na sygnał od głównego wątku, aby rozpocząć pracę.

**Kluczowe cechy `CountDownLatch`**
- *Jednokrotność* - Po osiągnięciu licznika 0 `CountDownLatch` nie może być ponownie użyty. Jeśli potrzebujesz wielokrotnego resetowania, użyj `CyclicBarrier`
- *Bezpieczeństwo wątkowe* - Operacje na liczniku są automatycznie synchronizowane
- *Prostota API* - Oferuje tylko kilka metod, co czyni go łatwym w użyciu