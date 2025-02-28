
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

### Podstawowa konfiguracja NGINX

Plik konfiguracyjny NGINX (najczęściej `/etc/nginx/nginx.conf`) ma strukturę podobną do tej:
```nginx
worker_processes auto; # Liczba procesów roboczych (automatyczna detekcja CPU)

events {
	worker_connections 1024; # Ile połączeń może obsłużyć jedne worker
}

http {
	server {
		listen 80; # Nasłuchuje na porcie 80 (HTTP)
		server_name example.com; # Nazwa domeny
		root /var/www/html; # Katalog z plikami do serwowania
		index index.html; # Domyślny plik startowy

		location / {
			try_files $uri $uri/ =404;
		}
	}
}
```

**Reverse Proxy - Przekierowanie ruchu do backendu**
Jeśli masz backend w Node.js, Django lub PHP, możesz skonfigurować NGINX jako reverse proxy:
```nginx
server {
	listen 80;
	server_name myapp.com;

	location / {
		proxy_pass http://127.0.0.1:3000; # Przekazuje żądania do backendu
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	}
}
```

### Porównanie NGINX z Apache

| Cecha                      | NGINX                         | Apache                                 |
| -------------------------- | ----------------------------- | -------------------------------------- |
| Model usługi               | Asynchroniczny                | Wielowątkowy                           |
| Obsługa statycznych plików | Szybsza                       | Wolniejsza                             |
| Konfiguracja               | Trudniejsza na początku       | Bardziej intuicyjna dla początkujących |
| Moduły                     | Mniej elastyczne, ale wydajne | Bardziej konfigurowalne                |
| Skalowalność               | Świetna                       | Dobra, ale wymaga tuningu              |
Apache nadal ma swoje zastosowania, zwłaszcza gdy korzystasz z `.htaccess`, ale jeśli zależy Ci na wydajności i skalowalności, NGINX jest lepszym wyborem.


