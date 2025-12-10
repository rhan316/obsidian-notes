
*Chodzi o to, żeby twój kod zależał od rzeczy, które mogą istnieć, a nie od konkretnych rzeczy, które muszą istnieć*
Czyli od interfejsów, a nie od konkretnych klas.

~={8}Kiedy piszesz `Car car = new Car();`=~
~={8}to przykuwasz cały swój kod do jednej implementacji. Zero swobody. Jak kajdanki.=~

~={12}**Ale kiedy piszesz `Vehicle car = new Car();` lub `Vehicle vehicle = factory.create();`**
to jesteś wolny. Twój kod nie wie i NIE MUSI wiedzieć, czy to jest: =~
- Car
- Truck
- HoverBike
- Albo implementacja testów, mock, gówno w papierku - cokolwiek. 

~={10}***To daje elastyczność, testowalność, wymienność implementacji i luźne sprzężenie***
Dokładnie to, czego potrzebujesz w dużych projektach, żeby potem nie siedzieć do 2:00 w nocy i płakać nad refaktoryzacją .=~

### Dlaczego to takie ważne?

Bo życie to piekło, a zmiana wymaga kosztów.
Gdy wszystko jest oparte na klasach:
- zmieniasz jedną klasę -> sypią się trzy moduły obok
- chcesz przetestować coś -> musisz przynieść pół produkcyjnej logiki
- chcesz podmienić implementację -> powodzenia, kurwa miłego refaktora.

**Interfejsy izolują te problemy.**

Design patterns typu Strategy, Adapter, Factory, Dependency Injection bazują dokładnie na tym - na zależności od abstrakcji.
I tak, zgadłeś: to jest powód, dla którego całe Springowe DI w ogóle działa.

W dokumentach, książkach o wzorcach projektowych jest to podstawowy fundament - programowanie do interfejsów daje bardziej modularny, elastyczny kod.

---
Wyobraź sobie, że masz system płatności:
```java
class PaymentProcessor {
	void pay() {
		PayPalClient client = new PayPayClient();
		client.process();
	}
}
```
Gratulacje użytkowniku - właśnie zabetonowałeś cały system do PayPala.
Chcesz podpiąć Stripe? Za tydzień Za miesiąc? Po migracji działu finansów?
**Boom, wszystko do przeróbki**

A gdybyś od początku pomyślał trochę i zrobił:
```java
interface PaymentClient {
	void process(); 
}

class PayPalClient implements PaymentClient { ... }
class StripeClient implements PaymentClient { ... }

class PaymentProcessor {
	private final PaymentClient client;
	
	PaymentProcessor (PaymentClient client) {
		this.client = client;
	}
	
	void pay() {
		client.process();
	}
}
```
To nagle:
- możesz wstrzykiwać cokolwiek,
- testować bez bólu,
- zmieniać implementacje bez połamania kręgosłupa kodu.

