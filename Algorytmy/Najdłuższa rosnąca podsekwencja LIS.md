Czym jest LIS?
Jest to tablica liczb całkowitych z podanej tablicy w porządku rosnącym, z zastrzeżeniem, że wszystkie elementy LIS powinny być ciągłe.
```java
Array => 15, -1, 8, 2, 5, 11, 7, 10
LIS => -1, 2, 5, 7, 10
```

```java
// WERSJA O(n^2)
public static int LISMemoize(int[] LISArray) {
	int len = LISArray.length;
	// Tablica pomocnicza: mem[i] = długość LIS kończącego się na indeksie i
	// Domyślnie 1, bo kazdy element sam w sobie tworzy podciąg o długości 1
	int[] mem = new int[len];
	
	// Inicjalizacja mem[] jedynkami
	for (int i = 0; i < len; i++) {
		mem[i] = 1;
	}
	
	// Dla każdego elementu LISArray[i] sprawdzamy wszystkie wcześniejsze LISArray[j] i jeśli LISArray[j] < LISArray[i], to znaczy że możemy wydłużyć rosnący podciąg.
	for (int i = 1; i < len; i++) {
		for (int j = 0; j < i; j++) {
			if (LISArray[j] < LISArray[i]) {
				mem[i] = Math.max(mem[i], mem[j] + 1);
			}
		}
	}
	
	// Znalezienie maksymalnej długości LIS w tablicy mem[]
	int max = mem[0];
	for (int i = 1; i < len; i++) {
		max = Math.max(mem[i], max);
	}
	// Zwracamy długość najdłuższego rosnącego podciągu
	return max;
}
```

```java
// WERSJA O(n log n)
public static int binaryLIS(int[] arr) {
	int len = arr.length;
	
	// binArr przechowuje najmniejsze możliwe wartości końcowe LIS-a.
	// dla każdej długości podciągu.
	// binArr[len] = minimalny możliwy ostatni element LIS o długości len+1.
	int[] binArr = new int[len];
	
	// Pierwszy element LIS-a to pierwszy element wejściowej tablicy.
	binArr[0] = arr[0];
	
	// index oznacza obecną długość LIS-a (czli liczbe użytych pozycji w binArr)
	int index = 1;
	
	for (int i = 1; i < len; i++) {
		// Jeśli aktualny element jest większy niż ostatni element aktualnego LIS-a
		// to możemy wydłużyć LIS - dopisujemy go na końcu.
		if (binArr[index - 1] < arr[i]) {
			binArr[index] = arr[i];
			index++;
		} else {
			// W przeciwnym razie trzeba znaleźć miejsce, w które można wstawić
			// arr[i], aby zastąpić większy element i obniżyć wartość końca
			// któregoś z podciągów. Binary search znajduję właściwą pozycję.
			int idxWhereCurrEle = Arrays.binarySearch(binArr, 0, index, arr[i]);
			
		//Jeśli element nie występuje, binarySearch zwraca -(insertionPoint) - 1.
		// Trzeba to przekształcić na właściwy insertionPoint.
			if (idxWhereCurrEle < 0) {
				idxWhereCurrEle = (-idxWhereCurrEle) - 1;
			}
			// Podmieniamy element - obniżamy wartość końca podciągu,
			// nie zmieniając jego długości.
			binArr[idxWhereCurrEle] = arr[i];
		}
	}
}
```

