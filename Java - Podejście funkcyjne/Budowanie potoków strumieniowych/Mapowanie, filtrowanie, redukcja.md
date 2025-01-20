
|             |                        |
| ----------- | ---------------------- |
| Mapowanie   | Przekształcanie danych |
| Filtrowanie | Wybór danych           |
| Redukcja    | Wyprowadzanie wyniku   |

```
int totalNumbers = numbers.stream()  
	.peek(e -> System.out.println("Elemtent: " + e))  
	.reduce(0, Integer::sum);  
  
var words = List.of("banan", "pomarańcza", "jabłko", "śliwka", "gruszka");  
  
var wordsResult = words.stream() // Tworzenie strumienia ze źródła danych  
		.map(element -> element + ": " + element.length()) // Mapowanie =>  Przekształcanie danych  
	.filter(element -> element.length() > 9) // Filtrowanie => Wybór danych  
	.toList(); // Redukcja => Wyprowadzenie wyniku  
  
wordsResult.forEach(System.out::println);
```