Przy usuwaniu węzła istnieją 3 różne przypadki, które trzeba obsłużyć osobno:
1. **Usuwanie węzła bez dzieci (węzła)**.
2. **Usunięcie węzła z jednym dzieckiem.
3. **Usunięcie węzła z dwójką dzieci (najtrudniejszy przypadek).


#### Usunięcie węzła bez dzieci (liść)
```
    50
   /  \
  30   70
 /  
20   
Jeśli usuniemy 20, po prostu ustawiamy root.left = null.
```

#### Usunięcie węzła z jednym dzieckiem
```
Jeśli węzeł ma jedno dziecko, podmieniamy go na to dziecko.

    50
   /  \
  30   70
    \
    40
Jeśli usuniemy 30, jego prawe dziecko 40 zajmie jego miejsce.
```

#### Usunięcie węzła z dwójką dzieci (najtrudniejsze)
```
Jeśli węzeł ma dwójkę dzieci, musimy znaleźć jego następce i zastąpić nim węzeł.
Usuwamy 50

    50
   /  \
  30    70
    \  /
  40  60

Krok 1: Znajdujemy następcę in-order (najmniejszy element w prawym poddrzewie-> 60)
Krok 2: Zastępujemy 50 wartością 60
Krok 3: Usuwamy 60 z jego poprzedniej pozycji

Drzewo po usunięciu 50

    60
   /  \
  30   70
     \
     40

```

---
```java
private Node<T> deleteRec(Node<T> root, T value) {
	if (root == null) return null;

	if (comparator.compare(value, root.data)) < 0) {
		root.left = deleteRec(root.left, value);
	} else if (comparator.compare(value, root.data > 0)) {
		root.right = deleteRec(root.right, value);
	} else {

		// Przypadek: Węzeł bez dzieci
		if (root.left == null && root.right == null) {
			return null;
		}

		// Przypadek: Węzeł z jednym dzieckiem
		if (root.left == null) {
			return root.right;
		}

		if (root.right == null) {
			return root.left;
		}

		// Przypadek: Węzeł z dwójką dzieci
		root.data = minValue(root.right); // Znajdujemy najmniejszy element w prawym poddrzewie
		root.right = deleteRec(root.right, root.data); // Usuwamy ten element
	}

	return root;
}
```