Kontener IoC (Inversion of Control) to serce frameworka Spring. Mechanizm zarządzający tworzeniem, konfiguracją i cyklem życia obiektów w aplikacji. Dzięki niemu programiści mogą skupić się na logice biznesowej, a zarządzanie zależnościami jest automatyzowane.

---
***Co to jest Inversion of Control (IoC)?***
	IoC (Inversion of Control) to wzorzec projektowy, który odwraca tradycyjny sposób zarządzania zależnościami. Zamiast tworzyć obiekty w kodzie i zarządzać ich zależnościami ręcznie, programiści oddają tę odpowiedzialnośc kontenerowi IoC:
		Tworzy obiekty (bean'y)
		Inicjalizuje ich zależności
		Zarządza ich cyklem życia

---
***Dlaczego IoC?***
	W tradycyjnym podejściu programista tworzy obiekty ręcznie, co prowadzi do silnego powiązania kodu - klasy są mocno zależne od siebie, co utrudnia ich testowanie i ponowne użycie oraz problemy z skalowalnością - zarządzanie złożonymi zależnościami staje się trudne.
	**Podejście IoC**
		Obiekty (Beany) nie są odpowiedzialne za tworzenie swoich zależności - dostarczane są im przez kontener oraz zmniejsza się sprzężenie między komponentami.

---
***Jak działa IoC w Spring?***
	Spring implementuje IoC za pomocą kontenera IoC, który zarządza bean'ami. Proces ten odbywa się w 3 głównych krokach:
	~={green}**Definicja beanów**=~ - Beany są definiowane w kodzie (adnotacje), plikach konfiguracyjnych XML lub klasach konfiguracyjnych (Java Config).
	~={green}**Tworzenie beanów**=~ - Kontener IoC automatycznie tworzy obiekty, które zarejestrowane są jako beany.
	~={green}**Wstrzykiwanie zależności**=~ - Kontener dostarcza zależności wymagane przez beany.

---
***Kluczowe komponenty IoC w Spring***

1. **Bean** - obiekt zarządzany prze kontener IoC Spring. Definiowany w kontekście aplikacji i może mieć zależności od innych beanów.
2. **ApplicationContext** - Główny interfejs IoC w Spring. Odpowiedzialny za:
	- Zarządzanie cyklem życia beanów.
	- Wstrzykiwanie zależności.
	- Obsługę zdarzeń i kontekstów.
3. **Dependency Injection (DI)** - Mechanizm, który pozwala na dostarczenie zależności (np. innych beanów) do obiektu. Spring oferuje 3 typy obsługi DI ale **wstrzykiwanie przez konstruktor** jest zalecany.

---
