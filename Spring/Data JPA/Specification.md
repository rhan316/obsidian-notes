1. **Dynamiczne zapytania** --> Pozwala na tworzenie warunków zapytań w czasie wykonywania aplikacji, np. w zależności od danych wejściowych użytkownika.
2. **Łatwe łączenie warunków** --> Możesz łączyć wiele warunków za pomocą metod *and, or* i innych operacji logicznych.
3. **Reużywalność** --> Specyfikacje można ponownie wykorzystać w różnych miejscach aplikacji.
4. **Czytelność** --> Rozdzielenie logiki zapytań od reszty aplikacji poprawia organizację i czytelność kodu.

**Podstawowe pojęcia**
*Specification Interface*: Reprezentuje specyfikację zapytania. Jest to interfejs funkcyjny, który przyjmuje parametry:
- `Root<T>` Reprezentuje encję, na której operujemy.
- `CriteriaQuery<?>` Reprezentuje strukturę zapytania.
- `CriteriaBuilder` Narzędzie do tworzenia predykatów i modyfikacji zapytań.

Interfejs **Specification< T >** znajduje się w pakiecie `org.springframework.data.jpa.domain` i jest generycznym interfejsem, gdzie `<T>` reprezentuje typ encji, od której odnosi się zapytanie.

```
@FunctionalInterface
public interface Specification<T> extends Serializable {
	Predicate toPredicate(Root<T> root, CiteriaQuery<?> query, CriteriaBuilder b);
}
```

**Łączenie specyfikacji**
Specyfikacje można łączyć za pomocą metod:
- `Specification.where()` - ustawia podstawową specyfikację.
- `and()` - łączy dwie specyfikację za pomocą logicznego AND.
- `or()` - łączy dwie specy za pomocą logicznego OR.

```
Spec<Product> complexSpec = Spec.where(ProductSpec.hasCategory("Electronics"))
	.and(ProductSpec.hasPriceGreaterThan(500.0))
	.or(ProductSpec.hasNameContaining("Phone"));

List<Product> result = productRepo.findAll(complexSpec);
```

**Praktyczne zastosowania**
- Filtrowanie danych na podstawie wielu dynamicznych kryteriów.
- Budowa wyszukiwarki z różnorodnymi filtrami.
- Tworzenie bardziej skomplikowanych zapytań w dużych aplikacjach.