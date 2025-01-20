
Rachunek lambda służy do badania obliczeń i funkcji matematycznych. Jest podstawą wielu współczesnych teorii programowania i modelu obliczeń, a także ma ścisły związek z teorią funkcji i logiką matematyczną.

Główne pojęcia rachunki lambda


|                            |                                                                                                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Zmienne                    | Symboliczne reprezentacje wartości np. x, y, z                                                                                                                        |
| Funkcje(abstrakcje lambda) | Wyrażenie lambda definiuje funkcję np. λx.x+1 oznacza funkcję która przyjmuje argument x i zwraca x+1. Operator  λ wprowadza zmienną, która będzie argumentem funkcji |
| Aplikacje                  | Zastosowanie funkcji do argumentu, np.  ( λx. x+1) 5 oznacza użycie funkcji  λx. x+1 z argumentem 5, co daje 6                                                        |
| Redukcja                   | Proces upraszczania wyrażeń lambda przez podstawienie wartości argumentu w funkcji, np. redukcja ( λx. x+1) 5 do 5+1, co daje wynik 6. Nazywa się to beta-redukcja    |
```
(λx. x * 2) 
Funkcja dla argumentu x zwraca x * 2, gdy podamy do niej argument 3, otrzymamy:
(λx. x * 2) 3
3 * 2 = 6
```

Programista obiektowy jest przyzwyczajony do **programowania imperatywnego***, w którym za pomocą sekwencji instrukcji instruuje się komputer, co ma zrobić, aby wykonać określone zadanie.

Styl programowania funkcyjnego oferuje styl deklaratywny, prowadzający logię obliczeń bez opisywania ich rzeczywistego przepływu sterowania.

W deklaratywnym stylu programowania opisuje się wynik i sposób, w jaki program powinien pracować z wyrażeniami zamiast opisywania tego, co program powinien zrobić z instrukcjami.

Wyrażenie to sekwencja operatorów, operandów i wywołań metod.
```
value == null ? true : false
Operatory: == i ? :
Operandy: value, null, true, false
```