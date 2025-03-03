Niektóre zagadki są łatwe i możesz je szybko rozwiązać.
Inne są trudniejsze - możesz łatwo sprawdzić, czy dane rozwiązanie jest poprawne, ale znalezienie go samodzielnie zajęłoby ci bardzo dużo czasu.
Są też zagadki ekstremalnie trudne, których nawet sprawdzenie jest skomplikowane.

Na tej podstawie możemy podzielić problemy w informatyce na klasy `P, NP, NP-Complete i NP-Hard`

### P - Problemy łatwe do rozwiązania
"Łatwe" oznacza, że komputer może je rozwiązać szybko, czyli w czasie wielomianowym.
Przykład: Sortowanie liczb.
Czas działania: `O(n log n)` dla quicksort - szybko
To jak zagadka, którą możesz rozwiązać w kilka sekund bez większego wysiłku.

### NP - Problemy łatwe do sprawdzenia, ale trudne do rozwiązania
Nie wiadomo, czy da się je rozwiązać szybko, ale jeśli ktoś poda ci odpowiedź, możesz ją szybko sprawdzić.
Przykład: Sudoku
Czas działania: Znalezienie rozwiązania może być trudne, ale jak już ktoś ci je poda, to możesz sprawdzić w czasie `O(n^2)`, czy wszystkie liczby pasują.

To jak zagadka, którą musiałbyś spróbować rozwiązać metodą prób i błędów, ale jeśli ktoś poda ci odpowiedź, możesz ją szybko zweryfikować.
*Czy istnieje sposób na znalezienie rozwiązania dla wszystkich problemów NP?* To jest właśnie problem `P vs NP`

### NP-Complete - Problemy najtrudniejsze w NP
Są tak trudne, że jeśli znajdziesz szybki sposób na ich rozwiązanie, to rozwiążesz wszystkie problemy NP.
Przykład: Problemy plecakowy (Knapsack problem)
Czas działania: Brak znanego algorytmu działającego w czasie wielomianowym.

To jak najbardziej podchwytliwe zagadki w twoim mieście - jeśli ktoś wymyśli sposób na rozwiązanie jeden z nich szybko, to każda inna zagadka NP też stanie się łatwa!

### NP-Hard - Problemy jeszcze trudniejsze niż NP
Są co najmniej tak trudne jak NP-Complete, ale nie muszą być nawet w NP (czyli nie zawsze da się sprawdzić ich rozwiązanie szybko).
Przykład: Problem obchodzenia wież w szachach (General Chess Problem)
Czas działania: Może być nawet `superexponentialy`

To jak zagadka, której nawet nie jesteś w stanie zweryfikować, gdy ktoś poda ci rozwiązanie - np. "Jak wygrać w szachach z dowolnej pozycji."


| Klasa         | Czy można zaleźć rozwiązanie szybko? | Czy można sprawdzić rozwiązanie szybko? |
| ------------- | ------------------------------------ | --------------------------------------- |
| `P`           | Tak                                  | Tak                                     |
| `NP`          | (nie wiemy)                          | Tak                                     |
| `NP-Complete` | (nie wiemy)                          | Tak                                     |
| `NP-Hard`     | (raczej nie)                         | (może nie da się sprawdzić szybko)      |
