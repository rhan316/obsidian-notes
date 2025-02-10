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
