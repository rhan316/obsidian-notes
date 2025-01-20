Conversion w Spring Framework odnosi się do mechanizmu konwersji danych między różnymi typami. Jest to istotne w aplikacjach, gdzie dane przychodzą w jednym formacie (np. jako String z żądania HTTP) i muszą zostać przekształcone na odpowiedni typ w aplikacji (np. int, Date, obiekt domenowy).

`Converter` -> Interfejs do definiowania własnych konwerterów.
`ConversionService` -> Centralny interface odpowiedzialny za rejestrację i wykonywanie konwersji.
`Formatter` -> Rozszerza `Converter` o wsparcie dla lokalizacji (np. formatowanie dat i liczb w zależności od regionu).

---
***Dlaczego Conversion jest potrzebne?***
Wyobraź sobie, że użytkownik wprowadza dane w formularzu lub przesyła je jako parametry URL. Te dane zawsze przychodzą jako tekst (String). Jeśli aplikacja wymaga pracy z innymi typami danych (np. int, LocalDate, własnymi obiektami), musisz te dane przekonwertować.

---
***Najczęstsze pytania na rozmowach kwalifikacyjnych***


| Pytanie                                                                | Odpowiedź                                                                                                                                                      |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Co to jest Conversion w Spring?                                        | Conversion to mechanizm konwersji danych między typami, zarządzany przez `ConversionService`.                                                                  |
| Jak zarejestrować własny konwerter w Spring?                           | Możesz utworzyć klasę implementującą `Converter<S, T>` i zarejestrować ją w `ConversionService`.                                                               |
| Jaka jest różnica między `Converter` a `PropertyEditor` ?              | `Converter` jest nowoczesnym mechanizmem konwersji, natomiast `PropertyEditor` pochodzi z wcześniejszych wersji Spring i nie jest bezpieczny dla wielu wątków. |
| Jak działa Conversion w przypadku `@RequestParam` lub `@PathVariable`? | Spring automatycznie używa konwerterów z `ConversionSerivce`, by przekształcić dane wejściowe (String) na odpowiedni typ (np. int, LocalDate, User)            |
| Czy mogę dodać niestandardowe konwertery w Spring Boot?                | Tak, możesz zarejestrować konwerter jako komponent `@Component` lub ręcznie dodać go do `ConversionService`.                                                   |
| Jak Spring konwertuje dane z URL'a do obiektów?                        | Spring automatycznie używa `ConversionService` do mapowania danych z URL na odpowiednie typy                                                                   |

---
Przykładowa implementacja konwertera
```
public class StringToIntegerConverter implements Converter<String, Integer> {
    @Override
    public Integer convert(String source) {
        return Integer.valueOf(source);
    }
}
```

---
Rejestracja konwerterów w Spring

1. `DefaultConversionService` to gotowa implementacja `ConversionService`, która zawiera zestaw domyślnych konwerterów (np. String -> int, String -> LocalDate).
2. Custom ConversionService Możesz zarejestrować własne konwertery w aplikacji.
```
@Configuration
public class ConversionConfig {

    @Bean
    public ConversionService conversionService() {
        DefaultConversionService service = new DefaultConversionService();
        service.addConverter(new StringToIntegerConverter());
        service.addConverter(new StringToLocalDateConverter());
        return service;
    }
}
```
3. Automatyczna konfiguracja w Spring Boot - SB automatycznie rejestruje konwertery w `ConversionService`. Możesz także użyć adnotacji `@Component`.