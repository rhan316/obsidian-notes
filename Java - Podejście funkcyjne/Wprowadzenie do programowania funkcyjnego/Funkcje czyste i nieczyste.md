Funkcje czyste mają dwie podstawowe zasady:
1. Te same dane wejściowe zawsze generują ten sam wynik. Wartość zwracana funkcji czystej musi zależeć wyłącznie od jej argumentów wejściowych.
2. Wystarczalność bez żadnego efektu ubocznego. Kod nie może wpływać na inne podmioty w programie.

```
Funkcja czysta:
public String toLowerCase(String str) {
	return str.toLowerCase();
}

Funkcja nieczysta:
public String buildGreeting(String name) {
	var now = LocalTime.now();
	return now.getHour() < 12 ? "Dzień dobry, " + name : "Witaj, " + name;
}
```

Referencyjna transparentność

Oznacza funkcję zwracającą ten sam wynik dla tych samych argumentów i nie ma żadnych efektów ubocznych.
```
public int sum(int a, int b) {
	return a + b;
}

Funkcja sum jest referencyjnie transparentna, bo:
1. Zawsze zwróci tę samą wartość dla tych samych argumentów
2. Nie ma efektów ubocznych, takich jak zmiana stanu zewnętrznego programu
```

|                       |                                                                                                                             |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Łatwiejsze testowanie | Funkcje referencyjne transparentne są łatwiejsze do testowania, ponieważ nie zależą do zewnętrznego stanu                   |
| Optymalizacja         | Kompilatory mogą bezpiecznie optymalizować kod, zastępując wywołania funkcji jej wynikami(technika znana jako memoizacja)   |
| Przewidywalność       | Funkcje te nie mają efektów ubocznych i zawsze zwracają ten sam wynik, są bardziej przewidywalne i łatwiejsze w debugowaniu |
