1. ***Bubble Sort (Sortowanie bąbelkowe)***
	- *Opis:* Prostota, ale niska wydajność. Przechodzi przez listę wiele razy, porównując sąsiadujące elementy i zamieniając je miejscami, jeśli są w złej kolejności.
	- *Złożoność czasowa:* O(n2).
	- *Kiedy stosować?* Małe dane, edukacja.
	
2. ***Insertion Sort (Sortowanie przez wstawianie)***
	- *Opis:* Wstawia każdy element w odpowiednie miejsce w posortowanej części.
	- *Złożoność czasowa:* O(n2) w pesymistycznym przypadku, O(n) dla prawie posortowanych danych.
	- *Kiedy stosować?* Małe zbiory danych lub prawie posortowane dane.

3. ***Merge Sort (Sortowanie przez scalanie)***
	- *Opis:* Dzieli dane na mniejsze podzbiory, sortuje je i scala w posortowaną całość.
	- *Złożoność czasowa:* O(n log n).
	- *Kiedy stosować?* Duże dane, stabilność sortowania jest wymagana.

4. ***Quick Sort (Sortowanie szybkie)***
	- *Opis* Wybiera pivot, dzieli dane na mniejsze i większe od pivot, sortuje każdą z grup.
	- *Złożoność czasowa* O(n log n) średnio, O(n2) w pesymistycznym przypadku
	- *Kiedy stosować?* Uniwersalne, ale unikać w przypadku dużej liczby identycznych elementów

5. ***Heap Sort (Sortowanie przez kopcowanie)***
	- *Opis* Tworzy kopiec binarny, a następnie iteracyjnie wybiera największy element
	- *Złożoność czasowa* O(n log n)
	- *Kiedy stosować?* Sortowanie w miejscu, brak potrzeby stabilności


| Algorytm       | Stabilność | Złożoność czasowa | Zastosowanie                  |
| -------------- | ---------- | ----------------- | ----------------------------- |
| Bubble Sort    | Tak        | O(n2)             | Małe dane, edukacja           |
| Insertion Sort | Tak        | O(n2)             | Małe, prawie posortowane dane |
| Merge Sort     | Tak        | O(n log n)        | Duże dane, stabilność         |
| Quick Sort     | Nie        | O(n log n)        | Uniwersalne                   |
| Heap Sort      | Nie        | O(n log n)        | Efektywność pamięci           |
