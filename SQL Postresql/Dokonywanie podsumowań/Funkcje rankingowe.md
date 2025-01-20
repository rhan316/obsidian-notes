Pozwalają na numerowanie, rankingowanie i analizowanie wyników w zestawieniach danych.

ROW_NUMBER()
Zwraca unikalny numer dla każdego wiersza w zestawie wyników, zaczynając od 1. Nie dopuszcza remisów, nawet jeśli wartości w kolumnach sortujących są takie same.
```
SELECT 
	employee_name AS "Pracownik", 
	total_pay AS "Wynagrodzenie",
	ROW_NUMBER() OVER (ORDER BY total_pay DESC) AS "Ranking"
```
![[Pasted image 20241024092512.png]]

RANK()
Przypisuje rangę dla każdego wiersza, ale w przypadku remisów przyznaję tę samą rangę dla wierszy o tej samej wartości, a następnie przeskakuje liczby dla kolejnych wierszy
```
SELECT employee_name, total_pay,
	RANK() OVER (ORDER BY total_pay DESC) AS "Rank"
FROM sf_salaries;
```

DENSE_RANK()
Podobna do funkcji RANK(), ale nie pomija rang po remisie. Remisy są dozwolone, ale kolejne rangi nie są przeskakiwane.
Pracownicy z taką samą wartością w total_pay mają tę samą rangę, a kolejne miejsce będzie przypisane bez pomijania liczby (np. 1, 2, 2, 3)

PERCENT_RANK()
Oblicza rangę procentową w stosunku do całego zestawu wyników, w zakresie od 0 do 1. Jest oblicza na podstawie formuły: (RANK() - 1 / (liczba_wierszy -1))
