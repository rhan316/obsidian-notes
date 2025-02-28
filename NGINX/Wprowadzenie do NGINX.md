
***NGINX ma kilka głównych zastosowań***

**Serwer WWW (Web Server)**
Można go używać do serwowania statycznych plików, takich jak HTML, CSS, JS, obrazy czy filmy.
Działa znacznie wydajniej niż Apache w obsłudze dużej liczby jednoczesnych użytkowników.
Wykorzystuje model asynchroniczny i zdarzeniowy.

**Reverse Proxy**
Jeśli masz aplikację działającą w jakimś backendowym frameworku, NGINX może działać jako "pośrednik", który przekazuje żądania do aplikacji.
Dzięki temu aplikacja nie musi samodzielnie obsługiwać ruchu HTTP - NGINX robi to za nią i przekazuje tylko konkretne żądania.
Może również szyfrować ruch (SSL/TLS), co oznacza, że aplikacja nie musi się martwić o certyfikaty HTTPS.

