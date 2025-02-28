
***NGINX ma kilka głównych zastosowań***

**Serwer WWW (Web Server)**
Można go używać do serwowania statycznych plików, takich jak HTML, CSS, JS, obrazy czy filmy.
Działa znacznie wydajniej niż Apache w obsłudze dużej liczby jednoczesnych użytkowników.
Wykorzystuje model asynchroniczny i zdarzeniowy.

**Reverse Proxy**
Jeśli masz aplikację działającą w jakimś backendowym frameworku, NGINX może działać jako "pośrednik", który przekazuje żądania do aplikacji.
Dzięki temu aplikacja nie musi samodzielnie obsługiwać ruchu HTTP - NGINX robi to za nią i przekazuje tylko konkretne żądania.
Może również szyfrować ruch (SSL/TLS), co oznacza, że aplikacja nie musi się martwić o certyfikaty HTTPS.

**Load Balancer**
Jeśli masz wiele serwisów aplikacyjnych (np. kilka instancji Django lub Node.js), NGINX może rozdzielać ruch równomiernie między nimi.
Dzięki temu zwiększa się wydajność, a jeśli jeden serwer padnie, użytkownicy nadal będą obsługiwani prze inne.
Obsługuje różne algorytmy load balancing, np. round-robin (kolejno do każdego serwera) lub least connections (do serwera z najmniejszą liczbą połączeń).

**Cache (buforowanie)**
Może przechowywać w pamięci podręcznej odpowiedzi na popularne żądania, aby nie trzeba było ich generować za każdym razem.
Przyśpiesza to ładowanie stron i zmniejsza obciążenie serwerów backendowych.

### Jak działa NGINX - prosty model asynchroniczny

Większość serwerów WWW działa w modelu wielowątkowym. Oznacza to, że dla każdego nowego użytkownika serwer tworzy osobny wątek, co zużywa dużo pamięci RAM i CPU.

NGINX działa inaczej: używa modelu asynchronicznego i zdarzeniowego.
- Jeden główny proces (Master Process) zarządza kilkoma procesami roboczymi (Worker Processes).
- Każdy Worker Process obsługuje wiele żądań jednocześnie, zamiast tworzyć dla każdego nowe wątki.
- Dzięki temu serwer zużywa mniej zasobów i może obsłużyć dziesiątki tysięcy jednoczesnych połączeń.
- 
