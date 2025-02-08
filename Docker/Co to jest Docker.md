Docker to platforma, która umożliwia tworzenie, uruchamianie i zarządzanie kontenerami - lekkimi, przenośnymi środowiskami, które zawierają aplikację oraz wszystko, co jest jej potrzebne do działania (np. bibliotek, zależności, systemu plików). Dzięki temu aplikacje są odizolowane od środowiska, w którym są uruchamiane, co rozwiązuje problemy typu "u mnie działa, u ciebie nie działa".

Wyobraź sobie międzynarodowy transport towarów. Zamiast martwić się, czy towary z jednego kraju będą pasować do rozmiarów ciężarówek, pociągów czy statków w innym kraju, używamy standardowych kontenerów. Każdy kontener jest niezależny od środowiska transportowego, a jego zawartość (np. samochody, komputery, owoce) może być bezpiecznie transportowane w jednolity sposób.

W świecie technologii Docker robi coś podobnego:
- Tworzy *kontenery*, które zawierają aplikację i jej środowisko (biblioteki, konfiguracje)..
- Kontener działa tak samo niezależnie od tego, czy jest uruchomiony na Twoim laptopie, serwerze w chmurze czy w centrum danych.

---
***Kluczowe pojęcia w Dockerze***

1. ~={9}**Obraz (Image)**:=~ Obraz Docker to jak "przepis" na kontener. Zawiera instrukcję, jak skonfigurować środowisko i uruchomić aplikację. Przykładami obrazów mogą być: System operacyjny Ubuntu z Pythonem albo Serwer Apache z preinstalowaną aplikacją.
2. ~={9}**Kontener (Container)** =~- Kontener to uruchomiona instancja obrazu. Możesz traktować go jak "żywy" proces, który działa zgodnie z instrukcjami zawartymi w obrazie. Kontenery są: ~={blue}**Izolowane=~ (nie wpływają na inne aplikacje na serwerze) i~={blue} Lekkie=~ (działają szybko, ponieważ współdzielą zasoby z systemem gospodarza)**.
3. ~={9}**Dockerfile**:=~ Plik tekstowy, w którym opisujesz, jak zbudować obraz Dockera. Jest jak przepis kulinarny dla twojej aplikacji. Zawiera takie kroki jak: jakiej bazy systemu użyć (np. Ubuntu), jakie zależności zainstalować, jak uruchomić aplikacje itp.
4. ~={9}**Docker Hub**:=~ Publiczne repozytorium, w którym możesz znaleźć gotowe obrazy (np. `python`, `nginx`, `mysql`) lub przesłać swoje własne. To jak sklep z kontenerami, które możesz pobrać i użyć.

---
Docker korzysta z ~={9}technologii wirtualizacji =~, ale w przeciwieństwie do klasycznych maszyn wirtualnych, takich jak VMware, nie tworzy całego systemu operacyjnego. Zamiast tego Docker używa jądra hosta (Linux, Windows) i izoluje procesy w kontenerach.

| Cecha             | Docker                              | Maszyna wirtualna                 |
| ----------------- | ----------------------------------- | --------------------------------- |
| Czas uruchomienia | Sekundy                             | Minuty                            |
| Zużycie zasoób    | Lekkie (dzieli zasoby hosta)        | Cięższe (pełen system operacyjny) |
| Izolacja          | Dzieli jądro systemu                | Pełna izolacja                    |
| Przenośność       | Bardzo przenośny (kontener = obraz) | Mniej przenośna                   |
**Dlaczego Docker jest popularny?**
1. *Przenośność* - kontenery działają na każdym systemie z zainstalowanym Dockerem.
2. *Izolacja* - każda aplikacja działa w swoim własnym środowisku, więc konflikty zależności są eliminowane.
3. *Automatyzacja* - Docker integruje się z systemami CI/CD (np. Jenkins, GitHub Actions).
4. *Skalowalność* - Dzięki Dockerowi można łatwo skalować aplikacje w klastrach (np. Kubernetes).