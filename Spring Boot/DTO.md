DTO (ang. Data Transfer Object) to wzorzec projektowy używany do przesyłania danych między warstwami aplikacji. W kontekście Spring, DTO jest często stosowane do przysyłania danych między: 1. Warstwą kontrolera a klientem (np. REST API), 2. Warstwą usługową a kontrolerem.

DTO nie zawiera logiki biznesowej - jej celem jest wyłącznie transport danych.

**Dlaczego używamy DTO?**

| Powód                                                | Opis                                                                                                                                                       |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Oddzielenie modelu domenowego od warstw zewnętrznych | Chroni wewnętrzny model aplikacji (np. encje JPA) przed niepożądanym dostępem lub modyfikacją przez klienta. Ułatwia modyfikację modelu bez wpływu na API. |
| Minimalizacja przesyłanych danych                    | DTO może zawierać tylko te dane, które są wymagane w danym kontekście, co zmniejsza rozmiar żądań i odpowiedzi.                                            |
| Elastyczność                                         | DTO można dostosować do wymagań klienta, bez modyfikowania wewnętrznego modelu domenowego.                                                                 |
| Separacja odpowiedzialności                          | Każda warstwa aplikacji ma swoje odpowiednie obiekty danych, co większa modularność i czytelność kodu.                                                     |
```
Encja JPA
@Entity public class User { 
	@Id private Long id; 
	private String firstName; 
	private String lastName; 
	private String email;
	 
	// Gettery i settery 
}
```
```
DTO (Data Transfer Object)
public class UserDTO {
	private String firstName;
	private String lastName;
	private String email;
}
```