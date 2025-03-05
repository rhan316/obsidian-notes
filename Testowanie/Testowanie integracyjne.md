W Spring Boot to technika testowania, której celem jest sprawdzenie, czy różne komponenty aplikacji działają poprawnie razem. W przeciwieństwie do **testów jednostkowych**, które testują poszczególne klasy w izolacji, testy integracyjne sprawdzają współpracę między różnymi warstwami aplikacji - np. kontrolerami, serwisami, repozytoriami i bazą danych.

**Spring Boot oferuje wbudowane mechanizmy do testowania integracyjnego, które pozwalają na:"
- Uruchamianie całego kontekstu aplikacji (Spring Context) - testy działają w środowisku przypominającym rzeczywistą aplikację.
- Wstrzykiwanie komponentów Springa - np. serwisów czy repozytoriów.
- Symulowanie zapytań HTTP - za pomocą narzędzi takich jak `MockMvc` czy `TestRestTemplate`.
- Testowanie warstwy dostępu do danych - często z wykorzystywaniem bazy danych w pamięci, np. `h2`.
- Zachowanie izolacji testów - np. poprzez resetowanie bazy danych po każdym teście.

