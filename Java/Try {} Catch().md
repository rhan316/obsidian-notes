
Instrukcja try-catch w Javie służy do obsługi wyjątków, które mogą pojawić się podczas wykonywania programu. Wyjątki to sytuacji, które mogą przerwać normalne działanie programu, takie jak błędy w czasie wykonywania programu, np. próba podzielenia przez zero, dostęp do nieistniejącego elementu tablicy lub problem z odczytem pliku. Dzięki try-catch, można przechwycić i obsłużyć te błędy w kontrolowany sposób, co pozwala na zachowanie stabilności aplikacji.

Jeśli w bloku try może wystąpić więcej niż jeden rodzaj wyjątku, można dodać wiele bloków catch, aby przechwycić różne rodzaje wyjątków.

```
Instrukacja try-catch składa się z dwóch podstawowych części:
1. Blok try -> w tym bloku umieszczamy kod, który może potencjalnie zgłosić wyjątek
2. Blok catch -> przechwytuje wyjątki, które zostały zgłoszone w bloku try. Blok catch pozwala na zdefiniowanie sposobu obsługi błędu

try {
	int result = 10 / 0; => Próba podzielenia przez zero
} catch (ArithmeticException e) {
	System.out.println("Wystąpił błąd: " + e.getMessage());
}
System.out.prinln("Program kontynuuje działanie.");
```

Opcjonalny blok finally

Finally zawsze się wykona, niezależnie od tego, czy wyjątek został zgłoszony, czy nie. Jest używany do umieszczenia kodu, który powinien się wykonać zawsze, np. zamykanie zasobów czy połączenia z bazą danych.
```
try { 
	int[] numbers = {1, 2, 3}; 
	System.out.println(numbers[3]); // Próba dostępu do nieistniejącego indeksu }
	 
catch (ArrayIndexOutOfBoundsException e) { 
			System.out.println("Wystąpił błąd: " + e.getMessage()); 
} 

finally {  
System.out.println("Ten blok wykona się zawsze, niezależnie od błędu."); 
}
```

Try-with-resources

W Javie  dostępna jest także konstrukcja try-with-resources, która pozwala na automatyczne zamknięcie zasobów, w takich jak pliki czy strumienie. Wymaga, aby zasób implementował interfejs AutoCloseable.

```
try (BufferedReader br = new BufferedReader(new FileReader("plik.txt"))) {
	String line;
	while ((line = br.readline()) != null) {
		System.out.println(line);
	}
} catch (IOException e) {
	System.out.println("Błąd podczas odczytu pliku: " + e.getMessage());
}
```