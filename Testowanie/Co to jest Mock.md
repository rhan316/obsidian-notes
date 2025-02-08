Chcesz przetestować swój samochód (aplikację), ale nie chcesz zużywać prawdziwego paliwa (baza danych, zewnętrzne API). Dlatego wlewasz "fałszywe paliwo" (mocki) i sprawdzasz, czy silnik (Twoja logika biznesowa) działa zgodnie z oczekiwaniami. Mockowanie to właśnie takie "fałszywe paliwo" - udajemy, że mamy dane lub serwisy, które zachowują się w określony sposób.

~={12}***Co to jest Mock?***=~
~={12}*Mock*=~ to *imitacja* prawdziwego obiektu w testach.
Wygląda jak prawdziwy obiekt, ale możesz go zaprogramować, by zachowywał się dokładnie tak, jak potrzebujesz.
Używając Mock, możesz izolować konkretną część kodu i testować ją bez zależności od innych komponentów.

---
***Dlaczego warto mockować w Spring Boot?***
Spring Boot to framework, który często integruje różne warstwy, np:
- warstwa kontrolera (Controller): odpowiada za obsługę żądań HTTP.
- warstwa serwisu (Service): zawiera logikę biznesową.
- warstwa repozytorium (Repository): komunikuje się z bazą danych.

Jeśli testujesz np. warstwę serwisu, nie chcesz, by test zależał od prawdziwej bazy danych - dlatego używasz mocków, aby przyśpieszyć testy, skupić się na tym, co naprawdę testujesz i unikasz problemów z zewnętrznymi zależnościami.

---
***Jak działa Mockowanie w Spring Boot?***

Framework Mockito: W Spring Boot używa się najczęściej **Mockito** - biblioteki, która pozwala tworzyć i zarządzać mockami.

Adnotacje Spring Boot: 
`@MockBean` - tworzy mocka i wstrzykuje go do Springowego kontekstu.
`@Mock` - tworzy mocka, ale nie integruje go automatycznie z Springiem.
`@InjectMocks` - wstrzykuje mocki do obiektu, który testujesz.

`when()`, `thenReturn()`, `doReturn()` - konfigurowanie zachowanie mocków.
`verify()` - weryfikacja wywołań metod mockowanych.

Używasz testów jednostkowych do testowania pojedynczych komponentów aplikacji. Mocki symulują zachowanie zależności, więc możesz skupić się na testowaniu wybranego komponentu.

---
```
@SpringBootTest
class MyServiceTest {
	@Mock
	private MyRepo repo;

	@InjectMocks
	private MyService service;

	@Test
	void shouldSaveEntity() {

		// given
		Entity entity = new Entity();
		when(repo.save(entity)).thenReturn(entity);

		// when
		service.saveEntity(entity);

		// then
		verify(repo).save(entity);
	}
}
```