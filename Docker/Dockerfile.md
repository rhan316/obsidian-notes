Plik `Dockerfile` to instrukcja budowy obrazu Docker - jest jak przepis na przygotowanie kompletnego środowiska uruchomieniowego dla aplikacji. Każda linia w pliku opisuje jedną czynność lub konfigurację, która jest wykonywana podczas budowania obrazu.

Przykładowy pełny plik Dockerfile
```
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

~={8}***FROM: Podstawa obrazu*** Np. `FROM python:3.9`=~
FROM określa podstawę, na której ma być zbudowany obraz. Można to porównać do wyboru bazy w przepisie kulinarnym: czy zaczynasz od gotowego ciasta francuskiego, czy robisz je od zera.
Tutaj `python:3.9` oznacza, że korzystamy z oficjalnego obrazu Docker'a zawierającego język Python w wersji 3.9.
To jak wybór już przygotowanego zestawu narzędzi (np. skrzynki z narzędziami). W tym przypadku mamy skrzynkę z Pythonem w określonej wersji.

~={10}***RUN: Wykonanie polecenia*** Np. `RUN pip install flask`=~
RUN wykonuje polecenie w środowisku obrazu podczas jego budowania. Tutaj instalujemy bibliotekę `flask` za pomocą menadżera pakietów `pip`.
To jak przygotowanie składników podczas gotowania - np. dodanie przypraw lub obranie ziemniaków. Każda linia RUN to kolejny krok przygotowawczy.

~={blue}***COPY / ADD: Kopiowanie plików*** Np. `COPY app.py /app/`=~
Kopiuje pliki z twojego lokalnego systemu plików (np. z katalogu projektu) do obrazu Docker'a.
Tutaj kopiujemy plik `app.py` do folderu `/app/` w obrazie Docker'a.
Jeśli pakujesz walizkę na wyjazd, to *COPY* to moment, w którym pakujesz swoje ulubione ubrania (czyli pliki) do walizki (obrazu Docker'a).

~={yellow}***WORKDIR: Ustawienie katalogu roboczego*** `WORKDIR /app`=~
Ustawia katalog, w którym będą wykonywane wszystkie kolejne instrukcje (np. kopiowanie plików, uruchamianie skryptów).
To jakbyś powiedział: "Teraz będę pracować przy tym konkretnym biurku". Wszystko, co robisz, dzieje się w tym miejscu, chyba że wyraźnie zmienisz biurko.

~={red}***CMD: Domyślne polecenie do uruchomienia*** Np. `CMD ["python", "app.py"]`=~
Określa domyślne polecenie, które będzie uruchamiane po starcie kontrolera z obrazu. Tutaj kontener uruchomi skrypt `app.py` za pomocą Python'a.
Potraktuj to jako instrukcja - Po wszystkim włącz silnik i jedź.

~={11}***EXPOSE: Otwarcie portu*** `EXPOSE 5000`=~
Informuje, że obraz Docker'a będzie nasłuchiwał na określonym porcie (w tym przypadku `5000`, np. na potrzeby serwera).
To jakbyś otworzył okno w domu, przez które sąsiedzi mogą z tobą rozmawiać. Port jest tym oknem, przez które aplikacja komunikuje się ze światem.

~={12}***ENV: Zmienna środowiskowa*** `ENV FLASK_ENV=development`=~
Definiuje zmienną środowiskową dostępną w kontenerze. Tutaj ustawiamy tryb uruchamiania aplikacji na `development`. 
To jak dostarczenie mapy przy instrukcji pracy, żeby ktoś wiedział, w jakim trybie ma działać.

~={9}***ENTRYPOINT: Główne polecenie uruchomienia*** `ENTRYPOINT ["python"]`=~
Definiuje domyślne polecenie, które jest wykonywane w kontenerze. W przeciwieństwie do CMD, bardziej nakierowuje na ustalenie "domyślnego programu", np. uruchamianie tylko w Pythonie.
To jak określenie domyślnego narzędzia, które zawsze musisz używać, np. otwierasz plik tekstowy zawsze w Notatniku.





