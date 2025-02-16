Drzewa czerwono-czarne (Red-Black Trees) to jeden z kluczowych typów samobalansujących drzew binarnych wykorzystywany w informatyce. Znajdują zastosowanie w implementacjach zbiorów (Set) i map (Map) w Javie, np. w `TreeMap` oraz `TreeSet`.

Zanim przejdziemy do technicznych detali, wyobraź sobie drzewo jako sieć ulic w mieście, gdzie musimy utrzymać równowagę ruchu, aby nie było korków. Każda ulica (krawędź) prowadzi do skrzyżowania (węzła), a my musimy pilnować, aby wszystko działało płynnie. Kolory węzłów (czerwony/czarny) są jak sygnalizacja świetlna, która pomaga utrzymać równowagę.

---
#### Czym jest drzewo czerwono-czarne?

Drzewo czerwono-czarne to binarne posortowane drzewo (BST - Binary Search Tree) z dodatkowymi zasadami koloru węzłów, które zapewniają **samobalansowanie**.

**Właściwości drzew czerwono-czarnego**
1. Każdy węzeł ma kolor: czerwony lub czarny.
2. Korzeń (root) drzewa zawsze jest czarny. (Nie można zaczynać od czerwonego!)
3. Każdy liść (null pointer) jest traktowany jako czarny. (Chociaż technicznie liście mogą być NULL-em, w implementacji traktuje się je jako "niewidzialne" czarne węzły).
4. Jeśli węzeł jest czerwony, jego dzieci muszą być czarne. (Nie mogą być dwa czerwone węzły pod rząd - "zakaz korków na skrzyżowaniach").
5. Każda ścieżka od korzenia do liścia zawiera tyle samo czarnych węzłów. (To zapobiega powstaniu "krótkich i długich uliczek", które mogłyby spowodować zbyt duże nierównomierne rozłożenie węzłów).

Dzięki tym zasadom wysokość drzewa nigdy nie przekracza `2 log(n)`, co sprawia, że operacje `insert, delete i search` działają w `O(log n)`.

#### Wstawianie elementów do drzewa czerwono-czarnego

Dodawanie nowego elementu przypomina wprowadzenie nowego budynku do miasta - musimy przestrzegać zasad, aby utrzymać balans.
1. Wstawiamy nowy węzeł jak w zwykłym BST (Na właściwe miejsce zgodnie z zasadami `<=` i `>`).
2. Kolorujemy nowy węzeł na czerwono. (Nowe węzły są zawsze czerwone, bo jeśli dodalibyśmy czarny, zmienilibyśmy liczbę czarnych węzłów w ścieżce!).
3. Sprawdzamy, czy nie złamaliśmy zasad czerwono-czarnych.
	- Jeśli nowy węzeł ma czarnego ojca - wszystko jest w porządku.
	- Jeśli ojciec jest czerwony, mamy problem ("dwa czerwone węzły pod rząd" - to jak dwie sygnalizacje czerwone obok siebie, co powoduje chaos).
4. Naprawiamy drzewo (rebalansowanie)
	- Rotacje (lewa lub prawa) - zmieniamy strukturę drzewa, aby poprawić równowagę.
	- Przekolorowanie - zmieniamy kolory węzłów.

#### Rotacje (kluczowy mechanizm naprawczy)

Rotacje działają jak zmiana układu ulic, aby zlikwidować korki.
Rodzaje rotacji:
1. Rotacja w lewo - przesuwa poddrzewo w lewo.
2. Rotacja w prawo - przesuwa poddrzewo w prawo.

Wyobraź sobie, że mamy nierówne drzewo, gdzie jedna gałąź jest dłuższa - musimy przesunąć część ruchu na inną drogę, aby wyrównać długości tras.
```java
Node rotateLeft(Node x) {
	Node y = x.right;
	x.right = y.left;

	if (y.left != null) y.left.parent = x;
	y.parent = x.parent;

	if (x.parent == null) root = y;
	else if (x == x.parent.left) x.parent.left = y;
	else x.parent.right = y;

	y.left = x;
	x.parent = y;

	return y;
}

```
