# 📌 Rekurencyjne dodawanie węzła do drzewa BST w Javie

## 🔍 Opis metody `insertRec`

Metoda `insertRec` służy do **rekurencyjnego** dodawania nowego węzła do **drzewa binarnego poszukiwań (BST – Binary Search Tree)**.  
BST ma następujące właściwości:
- **Lewe poddrzewo** zawiera wartości **mniejsze** niż węzeł rodzica.
- **Prawe poddrzewo** zawiera wartości **większe** niż węzeł rodzica.

Metoda ta działa według prostego algorytmu:

1. **Jeśli drzewo jest puste**, tworzymy nowy węzeł i go zwracamy.
2. **Jeśli wartość jest mniejsza** od wartości w bieżącym węźle, rekurencyjnie wstawiamy ją do lewego poddrzewa.
3. **Jeśli wartość jest większa**, rekurencyjnie wstawiamy ją do prawego poddrzewa.
4. **Gdy dotrzemy do pustego miejsca (`null`)**, tworzymy nowy węzeł.
5. **Rekurencja cofa się**, aktualizując węzły rodziców.

## 📝 Implementacja w Javie

```java
private Node<T> insertRec(Node<T> root, T value) {
    if (root == null) return new Node<>(value);

    if (comparator.compare(value, root.data) < 0) {
        root.left = insertRec(root.left, value);
    } else if (comparator.compare(value, root.data) > 0) {
        root.right = insertRec(root.right, value);
    }

    return root;
}
```


# 🔄 **Analiza działania kodu**

#### **Warunek bazowy (koniec rekurencji)**
`if (root == null) return new Node<>(value);`
Jeśli root jest nullem, tworzymy nowy węzeł i go zwracamy.
Zatrzymuje to rekurencję.

#### **Porównywanie wartości i wywoływanie rekurencyjne**
```java
if (comparator.compare(value, root.data < 0)) {
	root.left = insertRec(root.left, value);
} else if (comparator.compare(value, root.data > 0)) {
	root.right = insertRec(root.right, value);
}
```
Jeśli wartość jest mniejsza, idziemy w lewo.
Jeśli wartość jest większa, idziemy w prawo.
Jeśli trafimy na null, tworzymy nowy węzeł.





