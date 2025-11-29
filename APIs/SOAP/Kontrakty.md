*Contract-first* i *Contract-last* to dwa podejścia do tworzenia usług sieciowych (np. SOAP) i określają, jak podchodzi się do definiowania interfejsu usługi oraz jej implementacji. Są one kluczowe w kontekście technologii takich jak SOAP, gdzie najważniejszym elementem jest WSDL (Web Services Description Language).

**Contract-first**

1. **Opis** - W podejściu contract-first proces rozpoczyna się od zdefiniowania kontraktu (WSDL w przypadku SOAP), czyli dokładnego opisu interfejsu usługi. Dopiero na podstawie tego kontraktu tworzona jest implementacja usługi.
2. **Etapy**
	- Zdefiniowanie WSDL (lub XSD, jeśli kontrakt opisuje dane)
	- Generowanie kodu serwera i klienta na podstawie kontraktu
	- Implementacja logiki biznesowej
3. **Zalety**
	- Jasny i stabilny interfejs - Interfejs jest z góry określony i dobrze zdefiniowany
	- Łatwa współpraca - Klienci usługi mogą używać WSDL do integracji, niezależnie od implementacji
	- Lepsza kontrola nad strukturą XML i standardami

***Contract-last***

1. **Opis** - W podejściu contract-last implementacja usługi jest tworzona jako pierwsza, a kontrakt (WSDL) jest generowany automatycznie na podstawie kodu źródłowego
2. **Etapy**
	- Implementacja logiki biznesowej
	- Generowanie WSDL na podstawie implementacji (np. z użyciem frameworka jak Apache CXF lub JAX-WS)
3. **Zalety**
	- Szybki start - Można rozpocząć od kodu bez wcześniejszego tworzenia kontraktu
	- Dobre do prototypowania i wstępnych wersji aplikacji