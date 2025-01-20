Coalesce(arg1, arg2, ...)
Funkcja COALESCE akceptuje listę argumentów i zwraca pierwszy argument różny od NULL
```
COALESCE(1, 2) => 1
Ponieważ oba argumenty są różne od NULL, to funkcja zwraca 1

COALESCE(NULL, 2, 1) => 2
Pierwszy argument jest NULL, więc zwraca jest wartość 2
```
W praktyce COALESCE() jest często używana do podstawienia wartości domyślnej zamiast NULL podczas wykonywania zapytań dotyczących danych z kolumn dopuszczających wartości NULL.

NULLIF(arg1, arg2)
Funkcja NULLIF zwraca NULL, jeśli oba argumenty są równe, w przeciwnym razie zwraca argument arg1.
```
NULLIF(1, 1) => NULL
Dwa argumenty są sobie równe to zwraca NULL

NULLIF(1, 0) => 1
1 != 0 zwraca 1

NULLIF(null, 'rower') => NULL
```