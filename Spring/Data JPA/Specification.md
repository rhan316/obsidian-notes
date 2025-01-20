1. **Dynamiczne zapytania** --> Pozwala na tworzenie warunków zapytań w czasie wykonywania aplikacji, np. w zależności od danych wejściowych użytkownika.
2. **Łatwe łączenie warunków** --> Możesz łączyć wiele warunków za pomocą metod *and, or* i innych operacji logicznych.
3. **Reużywalność** --> Specyfikacje można ponownie wykorzystać w różnych miejscach aplikacji.
4. **Czytelność** --> Rozdzielenie logiki zapytań od reszty aplikacji poprawia organizację i czytelność kodu.

Interfejs **Specification< T >** znajduje się w pakiecie `org.springframework.data.jpa.domain` i jest generycznym interfejsem, gdzie `<T>` reprezentuje typ encji, od której odnosi się zapytanie.

```
@FunctionalInterface
public interface Specification<T> extends Serializable {
	Predicate toPredicate(Root<T> root, CiteriaQuery<?> query, CriteriaBuilder b);
}
```

