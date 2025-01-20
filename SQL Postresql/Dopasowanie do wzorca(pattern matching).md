
| LIKE                | Używany do dopasowania ciągu znaków, rozróżniając wielkość liter              | %  dowolna ilość znaków                                         | __  dokładnie jeden znak                                                    |                                                              |                                                 |                                   |
| ------------------- | ----------------------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- |
| ILIKE               | Wersja LIKE bez rozróżniania wielkości znaków                                 | jak w LIKE                                                      | jak w LIKE                                                                  |                                                              |                                                 |                                   |
| SIMILAR TO          | Obsługuje dopasowanie na podstawie wyrażeń regularnych                        | jak w LIKE                                                      | jak w LIKE                                                                  | \|  dopasowanie do jednego z wzorców                         | [zbiór_znaków] dokładnie jeden ze zbioru_znaków | [^zbiór_naków] znaki nie pasujące |
| Wyrażenia regularne | Obsługuje pełne wyrażenia regularne (regex) dla bardziej zaawansowanych zadań | ~ służy do dopasowania regularnego, wielkość liter ma znaczenie | ~* dopasowuje wyrażenie regularne bez znaczenia czy litery są duże lub małe | !~ !~* wersje negujące poprzednich wersji (jeśli nie pasuje) |                                                 |                                   |
1. LIKE: ``` SELECT * FROM users WHERE username LIKE 'J%'```
   (%J%) oznacza znalezienie danego znaku lub łańcucha znaków w każdym miejscu
   (%J) element musi kończyć się na J
   (J%) element musi zaczynać się na J
   (% J %) element musi znajdować się w środku w łańcuchu znaków 
```
2. ILIKE =>  SELECT * FROM users WHERE username ILIKE 'j%';

```
```
3. SIMILAR TO => SELECT * FROM orders WHERE order_code SIMILAR TO 'ORD[0-9]{3}|NEW%';

```
```
4. Wyrażenia regularne => SELECT * FROM users WHERE username ~ '^[A-Z]{3}[0-9]{2}$';

```