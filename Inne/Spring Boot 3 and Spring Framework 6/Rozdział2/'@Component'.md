**Czym jest @Component?**

To adnotacja w Springu, która oznacza, że dana klasa jest komponentem Spring'a.
Komponent to klasa zarządzana prze kontener Spring'a (tzw. Spring Context).
Spring automatycznie wykrywa klasy oznaczone @Component i rejestruje je jako beany w kontekście aplikacji podczas procesu skanowania komponentów (component scanning).

**Do czego służy @Component?**

Służy do deklarowania klasy jako kandydata na bean w kontenerze Spring'a.
Spring automatycznie tworzy instancje klasy (bean) i zarządza jej cyklem życia.
Dzięki tej adnotacji, można wstrzykiwać (injectować) obiekt tej klasy do innych klas, używając mechanizmu dependency injection (DI).

**Jak działa @Compoent?**

Spring podczas uruchamiania aplikacji skanuje pakiety w poszukiwaniu klas oznaczonych @Component.
Domyślnie skanowanie odbywa się w pakiecie głównym (tym, w którym znajduje się klasa @SpringBootApplication) oraz jego podpakietach.
Każda klasa oznaczona @Component jest automatycznie rejestrowana jako bean w Spring Context