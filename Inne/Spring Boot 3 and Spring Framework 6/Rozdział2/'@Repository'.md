**Do czego służy @Repository?**

Operacje na bazie danych:
- Klasy oznaczone @Repository są przeznaczone do obsługi operacji CRUD na bazie danych
- Mogą używać narzędzi, takich jak JPA, JDBC czy MyBatis
Obsługa wyjątków:
- Adnotacja ta automatycznie przekształca wyjątki związane z bazą danych (np. SQLException) w DataAccessException, czyli wspólne, abstrakcyjne wyjątki Springa.
- Dzięki temu kod jest bardziej niezależny od konkretnej technologii używanej do dostępu do danych
Liczne grupowanie:
- @Repository informuje programistów, że klasa jest odpowiedzialna za dostęp do danych
