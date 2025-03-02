**Backtracking** to technika algorytmiczna stosowana do rozwiązywania problemów poprzez stopniowe budowanie rozwiązania, gdy okazuje się, że dana ścieżka nie prowadzi do poprawnego wyniku. Jest używana w problemach kombinatorycznych, takich jak:
- Problem skoczka szachowego (Knight's Tour)
- Problem N-hetmanów (N-Queens)
- Rozwiązywanie sudoku
- Generowanie permutacji i kombinacji
- Problem plecackowy (w pewnych warunkach)

### Jak działa Backtracking?
*Intuicyjna analogia:*
Wyobraź sobie, że jesteś w labiryncie. Masz przed sobą wiele ścieżek.
1. Wybierasz jedną i idziesz nią tak daleko, jak tylko możesz.
2. Jeśli napotkasz ścianę (ślepy zaułek), cofasz się do ostatniego punku rozgałęzienia i wybierasz inną drogę.
3. Jeśli dojdziesz do wyjścia - sukces! Jeśli sprawdzisz wszystkie ścieżki i żadna nie działa, oznacza to, że rozwiązanie nie istnieje.
To dokładnie sposób działania algorytmu #Backtracking

### Struktura algorytmu #Backtracking 

1. Sprawdzanie warunku końcowego - Jeśli osiągnięto cel, zwróć wynik.
2. Spróbuj dostępnych opcji - Wybierz jeden z możliwych ruchów.
3. Sprawdź, czy wybór jest poprawny - Jeśli tak, przejdź do kolejnego kroku.
4. Rekurencyjnie przejdź dalej - Jeśli się udało - idź głębiej.
5. Jeśli trafisz na błąd, cofnij się (backtrack) - Usuń ostatni wybór i spróbuj kolejnej opcji.

### Implementacja w Javie
Rozważmy problem znalezienia permutacji ciągu znaków (np. `"ABC"` → `["ABC", "ACB", "BAC", "BCA", "CAB", "CBA"]`).
```java
String str = "ABC";
List<String> perm = new ArrayList<>();
backtrack("", str, perm);
print(perm);

static void backtrack(String pre, String rem, List<String> result) {
	if (rem.isEmpty()) {
		result.add(pre);
		return;
	}

	for (int i = 0; i < rem.len(); i++) {
		backtrack(
			pre + rem.charAt(i),
			rem.substring(0, i) + rem.substring(i + 1),
			result
		);
	}
} 
```
1. Start: `pre = ""`, `rem = "ABC`
2. Pierwsza iteracja: Dodajemy A, pozostaje "BC", następnie "B" i "C" -> "ABC"
3. Kolejna iteracja: Dodajemy A, ale zmieniamy kolejność pozostałych -> "ACB"
4. Cofamy się i próbujemy od B, potem C itd.
5. Kontynuujemy, aż sprawdzimy wszystkie permutacje

### Złożoność czasowa Backtracking
W najgorszym przypadku algorytmy backtracking mają eksponencjalną złożność czasową `O(k^n)`, gdzie `n` - to liczba decyzji do podjęcia, `k` - to liczba możliwych wyborów w każdym kroku.
Optymalizacje takie jak przycinanie gałęzi (np. w problemie N-Hetmanów sprawdzamy, czy hetman może być umieszczony) mogą zmniejszyć liczbę sprawdzonych przypadków.

### Podsumowanie
Backtracking działa jak eksploracja drzewa rozwiązań, w którym sprawdzamy wszystkie możliwości i cofamy się, gdy znajdziemy niepoprawną ścieżkę.
Świetnie nadaje się do problemów kombinatorycznych (np. sudoku, permutacje, problem hetmanów)
Często optymalizuje się go przez przycinanie gałęzi i heurystyki.

