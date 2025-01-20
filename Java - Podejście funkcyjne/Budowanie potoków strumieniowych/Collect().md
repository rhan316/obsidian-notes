```
List<String> namesStarsEndsWithR = nationalNames.stream()  
	.map(NationalNames::getName)  
	.distinct()  
	.filter(n -> n.startsWith("R") && n.endsWith("r"))  
	.filter(n -> n.length() == 5)  
	.collect(  
		ArrayList::new, => 1. Dostawca (supplier)  
		ArrayList::add,  => 2. Akumulator (accumulator)
		ArrayList::addAll => 3. Kombinator (combiner)
	);

1. Dostawca (ArrayList::new) => Tworzy nowy, pusty obiekt, w którym będą przechowywane wyniki. W każdej sesji strumienia, gdy proces redukcji rozpoczyna się, ta funkcja jest wywoływana, aby zainicjalizować nowy obiekt ArrayList

2. Akumulator(ArrayList::add) => Funkcja, która dodaje pojedyńczy element do wyniku redukcji (tutaj listy). Każdy element strumienia przechodzi przez filtry i inne operacje, jest dodawany do listy za pomocą tej metody.

3. Kombinator (ArrayList::addAll) => Łączy dwa obiekty wynikowe w przypadku równoległego przetwarzania strumienia. W równoległym strumieniu różne wątki mogą operowac na osobnych fragmentach danych i tworzyć własne częściowe wyniki. Kombinator zbiera te częściowe wyniki i scala je w jedną całość.
```